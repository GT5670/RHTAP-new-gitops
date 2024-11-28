git-clone
deploy-images
verify-enterprise-contract
gather-deploy-images
download-sbom-from-url-in-attestation
upload-sbom-to-trustification

Details of gather deploy images

apiVersion: tekton.dev/v1
kind: Task
metadata:
  name: gather-deploy-images
spec:
  description: Extract images from deployment YAML to pass to EC for validation
  workspaces:
    - description: Should contain a cloned gitops repo at the ./source subpath
      name: source
  params:
    - name: TARGET_BRANCH
      description: >
        If specified, will gather only the images that changed between
        the current revision and the target branch. Useful for pull requests.
        Note that the repository cloned on the source workspace must already
        contain the origin/$TARGET_BRANCH reference.
      type: string
      default: ""
    - name: ENVIRONMENTS
      description: Gather images from the manifest files for the specified environments
      type: array
      default: ["development", "stage", "prod"]
  results:
    - name: IMAGES_TO_VERIFY
      description: >
        The images to be verified, in a format compatible with
        https://github.com/konflux-ci/build-definitions/tree/main/task/verify-enterprise-contract/0.1.
        When there are no images to verify, this is an empty string.
  steps:
  - name: get-images-per-env
    image: quay.io/konflux-ci/appstudio-utils:48c311af02858e2422d6229600e9959e496ddef1@sha256:91ddd999271f65d8ec8487b10f3dd378f81aa894e11b9af4d10639fd52bba7e8
    workingDir: $(workspaces.source.path)/source
    env:
      - name: TARGET_BRANCH
        value: $(params.TARGET_BRANCH)
    args:
      - $(params.ENVIRONMENTS[*])
    script: |
      #!/bin/bash
      set -euo pipefail

      IMAGE_PATH='.spec.template.spec.containers[0].image'
      IMAGES_FILE='/tmp/all-images.txt'
      component_name=$(yq .metadata.name application.yaml)

      for env in "$@"; do
        yaml_path=components/${component_name}/overlays/${env}/deployment-patch.yaml
        image=$(yq "$IMAGE_PATH" "$yaml_path")

        if [ -n "$TARGET_BRANCH" ]; then
          prev_image=$(git show "origin/$TARGET_BRANCH:$yaml_path" | yq "$IMAGE_PATH")
          if [ "$prev_image" = "$image" ]; then
            # don't check images that didn't change between the current revision and the target branch
            continue
          fi
        fi

        printf "%s\n" "$image"
      done | sort -u > $IMAGES_FILE

      if [ ! -s $IMAGES_FILE ]; then
        echo "No images to verify"
        touch $(results.IMAGES_TO_VERIFY.path)
        exit 0
      fi

      # TODO: each component needs a {"source": {"git": {"url": "...", "revision": "..."}}}
      #       will that be too large for Tekton results?

      jq --compact-output --raw-input --slurp < $IMAGES_FILE '
        # split input file
        split("\n") |
        # drop empty lines
        map(select(length > 0)) |
        # convert into EC-compatible format
        {
          "components": map({"containerImage": .})
        }
      ' | tee $(results.IMAGES_TO_VERIFY.path)

Details of download-sbom-from-url-in-attestation.yaml

apiVersion: tekton.dev/v1
kind: Task
metadata:
  annotations:
    tekton.dev/tags: "sbom, attestation, cosign"
  name: download-sbom-from-url-in-attestation
spec:
  description: |-
    Get the SBOM for an image by downloading the OCI blob referenced in the image attestation.

    The input to this task (The `IMAGES` param) is a JSON string in the same format as the output
    of the [gather-deploy-images][gather-deploy-images] task:

        {
          "components": [
            {"containerImage": "<image reference>"},
            {"containerImage": "<image reference>"}
            ...
          ]
        }

    For each image, the task will:
    * Download the provenance attestation using `cosign verify-attestation`
    * Find the SBOM_BLOB_URL Tekton result in the attestation
    * Download the OCI blob referenced by the url.

    The task saves the SBOMs to `${SBOMS_DIR}/${image_reference}/sbom.json`. The image references
    are taken verbatim from the input object. For example, the output files could be:

        sboms-workspace/registry.example.org/namespace/foo:v1.0.0/sbom.json
        sboms-workspace/registry.example.org/namespace/bar@sha256:<checksum>/sbom.json

    [gather-deploy-images]: https://github.com/redhat-appstudio/build-definitions/tree/main/task/gather-deploy-images
  params:
  - name: IMAGES
    description: >-
      JSON object containing the array of images whose SBOMs should be downloaded.
      See the description for more details.
    type: string

  - name: SBOMS_DIR
    default: "."
    description: >-
      Path to directory (relative to the 'sboms' workspace) where SBOMs should be downloaded.
    type: string

  - name: HTTP_RETRIES
    default: "3"
    description: "Maximum number of retries for transient HTTP(S) errors"
    type: string

  - name: PUBLIC_KEY
    type: string
    description: >-
      Public key used to verify signatures. Must be a valid k8s cosign
      reference, e.g. k8s://my-space/my-secret where my-secret contains
      the expected cosign.pub attribute.
    default: ""

  - name: REKOR_HOST
    type: string
    description: Rekor host for transparency log lookups
    default: ""

  - name: IGNORE_REKOR
    type: string
    description: >-
      Skip Rekor transparency log checks during validation.
    default: "false"

  - name: TUF_MIRROR
    type: string
    description: TUF mirror URL. Provide a value when NOT using public sigstore deployment.
    default: ""
  workspaces:
  - name: sboms
    description: SBOMs will be downloaded to (a subdirectory of) this workspace.
  stepTemplate:
    env:
    - name: IMAGES
      value: $(params.IMAGES)
    - name: SBOMS_DIR
      value: $(workspaces.sboms.path)/$(params.SBOMS_DIR)
    - name: HTTP_RETRIES
      value: $(params.HTTP_RETRIES)
    - name: PUBLIC_KEY
      value: $(params.PUBLIC_KEY)
    - name: REKOR_HOST
      value: $(params.REKOR_HOST)
    - name: IGNORE_REKOR
      value: $(params.IGNORE_REKOR)
    - name: TUF_MIRROR
      value: $(params.TUF_MIRROR)
    - name: WORKDIR
      value: /tekton/home
  steps:
  - name: download-attestations
    image: quay.io/konflux-ci/appstudio-utils:48c311af02858e2422d6229600e9959e496ddef1@sha256:91ddd999271f65d8ec8487b10f3dd378f81aa894e11b9af4d10639fd52bba7e8
    script: |
      #!/usr/bin/env bash
      set -o errexit -o nounset -o pipefail

      if [[ -z "$PUBLIC_KEY" ]]; then
        echo "No public key set, cannot verify attestation." >&2
        exit 1
      fi

      cosign_args=(--key "$PUBLIC_KEY")

      if [[ -n "$REKOR_HOST" ]]; then
        cosign_args+=(--rekor-url "$REKOR_HOST")
      elif [[ "$IGNORE_REKOR" = "true" ]]; then
        cosign_args+=(--insecure-ignore-tlog)
      else
        cosign_args+=()
      fi

      if [[ -n "${TUF_MIRROR:-}" ]]; then
        echo 'Initializing TUF root...'
        cosign initialize --mirror "${TUF_MIRROR}" --root "${TUF_MIRROR}/root.json"
      fi

      jq -r '.components[].containerImage' <<< "$IMAGES" | while read -r image; do
        echo "Getting attestation for $image"
        mkdir -p "$WORKDIR/$image"
        cosign verify-attestation \
          --type slsaprovenance \
          "${cosign_args[@]}" \
          "$image" > "$WORKDIR/$image/attestation.json"
      done

  - name: download-sboms
    image: quay.io/konflux-ci/appstudio-utils:48c311af02858e2422d6229600e9959e496ddef1@sha256:91ddd999271f65d8ec8487b10f3dd378f81aa894e11b9af4d10639fd52bba7e8
    script: |
      #!/usr/bin/env bash
      set -o errexit -o nounset -o pipefail

      get_from_www_auth_header() {
          local www_authenticate=$1
          local key=$2
          # shellcheck disable=SC2001
          # E.g.
          #   www_authenticate='Bearer realm="https://ghcr.io/token",service="ghcr.io"'
          #   key=service
          #   -> ghcr.io
          sed "s/.*$key=\"\([^\"]*\)\".*/\1/" <<< "$www_authenticate"
      }

      get_container_auth() {
          # https://man.archlinux.org/man/containers-auth.json.5

          local image=$1

          local runtime_dir="${XDG_RUNTIME_DIR:-}"
          local config_home="${XDG_CONFIG_HOME:-$HOME/.config}"
          if [[ -n "$runtime_dir" ]]; then
              default_authfile="${runtime_dir}/containers/auth.json"
          else
              default_authfile="$config_home/containers/auth.json"
          fi

          local maybe_auth_files=(
              "$default_authfile"
              "$config_home/containers/auth.json"
              "$HOME/.docker/config.json"
              "$HOME/.dockercfg"
          )
          local auth_files=()
          for file in "${maybe_auth_files[@]}"; do
              if [[ -r "$file" ]]; then
                  auth_files+=("$file")
              fi
          done

          # registry.com/namespace/repo@sha256:digest -> registry.com/namespace/repo
          local auth_key=${image%@*}

          while true; do
              for auth_file in "${auth_files[@]}"; do
                  if jq -r -e --arg key "$auth_key" '.auths[$key].auth // empty' "$auth_file"; then
                      echo "Found auth for $auth_key in $auth_file" >&2
                      return 0
                  fi
              done

              # Try less specific key, e.g. registry.com/namespace/repo -> registry.com/namespace
              local new_key=${auth_key%/*}
              if [[ "$new_key" = "$auth_key" ]]; then
                  # Already tried all possible keys, no auth found
                  echo "No auth found for $auth_key" >&2
                  return 1
              fi

              auth_key=$new_key
          done

      }

      download_blob() {
        local blob_ref=$1
        local dest=$2

        # convert:
        #     registry.com/namespace/repo@sha256:digest
        # ->  https://registry.com/v2/namespace/repo/blobs/sha256:digest
        blob_url=$(sed -E 's;([^/]*)/(.*)@(.*);https://\1/v2/\2/blobs/\3;' <<< "$blob_ref")

        local tmp_dest
        tmp_dest=$(mktemp --tmpdir download-sbom-task.out.XXXXXX)

        local headers_file
        headers_file=$(mktemp --tmpdir download-sbom-task.headers.XXXXXX)

        local common_curl_opts=(--silent --show-error --retry "${HTTP_RETRIES:-3}")

        echo "GET $blob_url" >&2
        local response_code
        response_code=$(curl \
            "${common_curl_opts[@]}" \
            -L \
            --write-out '%{response_code}' \
            --output "$tmp_dest" \
            --dump-header "$headers_file" \
            "$blob_url"
        )

        if [[ "$response_code" -eq 200 ]]; then
            # Blob download didn't require auth, we're done
            :
        elif [[ "$response_code" -eq 401 ]]; then
            echo "Got 401, trying to authenticate" >&2

            local www_authenticate
            www_authenticate=$(sed -n 's/^www-authenticate:\s*//ip' "$headers_file")

            local realm service scope token_url
            realm=$(get_from_www_auth_header "$www_authenticate" realm)
            service=$(get_from_www_auth_header "$www_authenticate" service)
            scope=$(get_from_www_auth_header "$www_authenticate" scope)
            token_url=$(jq -n -r --arg realm "$realm" --arg service "$service" --arg scope "$scope" \
                '"\($realm)?service=\($service | @uri)&scope=\($scope | @uri)"'
            )

            local basic_auth token_auth
            if basic_auth=$(get_container_auth "$blob_ref"); then
                token_auth=(-H "authorization: Basic $basic_auth")
            else
                echo "Trying to get token anonymously" >&2
                token_auth=()
            fi

            echo "GET $token_url" >&2
            token=$(curl \
                "${common_curl_opts[@]}" \
                "${token_auth[@]}" \
                --fail \
                "$token_url" | jq -r .token
            )

            echo "GET $blob_url" >&2
            curl \
                "${common_curl_opts[@]}" \
                -L \
                --output "$tmp_dest" \
                --fail \
                -H "authorization: Bearer $token" \
                "$blob_url"
        else
            echo "Error: unexpected response code: $response_code!" >&2
            return 1
        fi

        cp "$tmp_dest" "$dest"
      }

      find_blob_url() {
          local attestation_file=$1

          jq -r --slurp < "$attestation_file" '
            map(
              .payload | @base64d | fromjson |
              .. | select(.name? == "SBOM_BLOB_URL") | .value // empty
            ) |
            unique |
            if length == 1 then
              first
            else
              error("Expected to find exactly one SBOM_BLOB_URL result, found \(length): \(.)")
            end'
      }

      jq -r '.components[].containerImage' <<< "$IMAGES" | while read -r image; do
          echo "Looking for SBOM_BLOB_URL result in the attestation for $image"
          attestation_file="$WORKDIR/$image/attestation.json"
          sbom_blob_url=$(find_blob_url "$attestation_file")
          mkdir -p "$SBOMS_DIR/$image"
          download_blob "$sbom_blob_url" "$SBOMS_DIR/$image/sbom.json"
      done

Details of upload-sbom-to-trustification.yaml
apiVersion: tekton.dev/v1
kind: Task
metadata:
  annotations:
    tekton.dev/tags: "sbom, trustification"
  name: upload-sbom-to-trustification
spec:
  description: |-
    Upload an SBOM file to [Trustification] using the [BOMbastic] API.

    [Trustification]: https://github.com/trustification/trustification
    [BOMbastic]: https://github.com/trustification/trustification/tree/main/bombastic

    ## Configuration

    This task requires some configuration and authentication secrets. By default, the task takes
    them from a secret called `trustification-secret` that exists in the same namespace where the
    task runs. You can override the secret name via the `TRUSTIFICATION_SECRET_NAME` param.

    ### trustification-secret

    Required keys:
    - bombastic_api_url: URL of the BOMbastic api host (e.g. https://sbom.trustification.dev)
    - oidc_issuer_url: URL of the OIDC token issuer (e.g. https://sso.trustification.dev/realms/chicken)
    - oidc_client_id: OIDC client ID
    - oidc_client_secret: OIDC client secret

    Optional keys:
    - supported_cyclonedx_version: If the SBOM uses a higher CycloneDX version,
        `syft convert` to the supported version before uploading.
  params:
  - name: SBOMS_DIR
    default: "."
    description: >-
      Directory containing SBOM files. The task will search for CycloneDX JSON
      SBOMs recursively in this directory and upload them all to Trustification.
      The path is relative to the 'sboms' workspace.
    type: string
  - name: HTTP_RETRIES
    default: "3"
    description: "Maximum number of retries for transient HTTP(S) errors"
    type: string
  - name: TRUSTIFICATION_SECRET_NAME
    default: trustification-secret
    description: Name of the Secret containing auth and configuration
    type: string
  - name: FAIL_IF_TRUSTIFICATION_NOT_CONFIGURED
    default: "true"
    description: >-
      Should the task fail if the Secret does not contain the required keys?
      (Set "true" to fail, "false" to skip uploading and exit with success).
    type: string
  workspaces:
  - name: sboms
    description: Directory containing the SBOMs to upload
  volumes:
  - name: trustification-secret
    secret:
      secretName: $(params.TRUSTIFICATION_SECRET_NAME)
      optional: true
  stepTemplate:
    env:
    - name: SBOMS_DIR
      value: $(workspaces.sboms.path)/$(params.SBOMS_DIR)
    - name: HTTP_RETRIES
      value: $(params.HTTP_RETRIES)
    - name: TRUSTIFICATION_SECRET_NAME
      value: $(params.TRUSTIFICATION_SECRET_NAME)
    - name: TRUSTIFICATION_SECRET_PATH
      value: /run/secrets/trustification
    - name: FAIL_IF_TRUSTIFICATION_NOT_CONFIGURED
      value: $(params.FAIL_IF_TRUSTIFICATION_NOT_CONFIGURED)
    - name: WORKDIR
      value: /tekton/home
    volumeMounts:
    - name: trustification-secret
      mountPath: /run/secrets/trustification
  steps:
  - name: gather-sboms
    image: quay.io/konflux-ci/appstudio-utils:48c311af02858e2422d6229600e9959e496ddef1@sha256:91ddd999271f65d8ec8487b10f3dd378f81aa894e11b9af4d10639fd52bba7e8
    script: |
      #!/usr/bin/env bash
      set -o errexit -o nounset -o pipefail

      version_lesser_equal() {
        local first
        first="$(printf "%s\n%s" "$1" "$2" | sort --version-sort | head -n 1)"
        [ "$1" = "$first" ]
      }

      if [[ -f "$TRUSTIFICATION_SECRET_PATH/supported_cyclonedx_version" ]]; then
        supported_version="$(cat "$TRUSTIFICATION_SECRET_PATH/supported_cyclonedx_version")"
      else
        echo "The '$TRUSTIFICATION_SECRET_NAME' secret does not set supported_cyclonedx_version, will not check SBOM versions"
        supported_version=""
      fi

      echo "Looking for CycloneDX SBOMs in $SBOMS_DIR"

      find "$SBOMS_DIR" -type f | while read -r filepath; do
        file_relpath=$(realpath "$filepath" --relative-base="$SBOMS_DIR")
        if ! jq empty "$filepath" 2>/dev/null; then
          echo "$file_relpath: not JSON"
          continue
        fi

        if ! jq -e '.bomFormat == "CycloneDX"' "$filepath" >/dev/null; then
          echo "$file_relpath: not a CycloneDX SBOM"
          continue
        fi

        echo "Found CycloneDX SBOM: $file_relpath"
        # The 'id' of each SBOM is checksum of the original content, before (possibly)
        # downgrading the CycloneDX version. The conversion always updates some metadata
        # (timestamp, UUID), changing the checksum. To avoid duplication, use the original
        # checksum.
        sbom_id="sha256:$(sha256sum "$filepath" | cut -d ' ' -f 1)"

        # Symlink the discovered SBOMS to ${WORKDIR}/${sbom_id}.json so that subsequent steps
        # don't have to look for them again.
        sbom_path="$WORKDIR/$sbom_id.json"
        ln -s "$(realpath "$filepath")" "$sbom_path"

        if [[ -n "$supported_version" ]]; then
          sbom_version="$(jq -r ".specVersion" "$sbom_path")"

          if version_lesser_equal "$sbom_version" "$supported_version"; then
            echo "SBOM version ($sbom_version) is supported (<= $supported_version), will not convert"
          else
            echo "SBOM version ($sbom_version) is not supported, will convert to $supported_version"
            printf "%s" "$supported_version" > "${sbom_path}.convert_to_version"
          fi
        fi
      done

      echo "Found $(find "$WORKDIR" -name "*.json" | wc -l) CycloneDX SBOMs"

  # Needs syft, which is in a different image => has to be a separate step
  - name: convert-sboms-if-needed
    image: registry.redhat.io/rh-syft-tech-preview/syft-rhel9:1.0.1@sha256:27c268d678103a27b6964c2cd5169040941b7304d0078f9727789ffb8ffba370
    script: |
      #!/usr/bin/env bash
      set -o errexit -o nounset -o pipefail

      # Return zero matches when a glob doesn't match rather than returning the glob itself
      shopt -s nullglob

      for sbom_path in "$WORKDIR"/*.json; do
        conversion_attr="${sbom_path}.convert_to_version"

        if [[ -f "$conversion_attr" ]]; then
          cdx_version="$(cat "$conversion_attr")"
          original_sbom_path="$(realpath "$sbom_path")"
          original_sbom_relpath="$(realpath "$sbom_path" --relative-base="$SBOMS_DIR")"

          echo "Converting $original_sbom_relpath to CycloneDX $cdx_version"
          syft convert "$original_sbom_path" -o "cyclonedx-json@${cdx_version}=${sbom_path}.supported_version"
        else
          # Just duplicate the symlink, the original SBOM already has a supported CDX version
          cp --no-dereference "$sbom_path" "${sbom_path}.supported_version"
        fi
      done

  - name: upload-sboms
    image: quay.io/konflux-ci/appstudio-utils:48c311af02858e2422d6229600e9959e496ddef1@sha256:91ddd999271f65d8ec8487b10f3dd378f81aa894e11b9af4d10639fd52bba7e8
    script: |
      #!/usr/bin/env bash
      set -o errexit -o nounset -o pipefail

      shopt -s nullglob
      sboms_to_upload=("$WORKDIR"/*.json)

      if [[ "${#sboms_to_upload[@]}" -eq 0 ]]; then
        echo "No SBOMs to upload"
        exit 0
      fi

      read_required_secret_key() {
        local key="$1"
        if [[ -f "$TRUSTIFICATION_SECRET_PATH/$key" ]]; then
          cat "$TRUSTIFICATION_SECRET_PATH/$key"
        else
          echo "Missing configuration: $key" >&2
          echo "Does the '$TRUSTIFICATION_SECRET_NAME' secret exist in your namespace and contain the required keys?" >&2
          echo "Refer to the description of this Task for details." >&2

          if [[ "$FAIL_IF_TRUSTIFICATION_NOT_CONFIGURED" == "false" ]]; then
            echo "WARNING: FAIL_IF_TRUSTIFICATION_NOT_CONFIGURED=false; exiting with success" >&2
            exit 0
          else
            exit 1
          fi
        fi
      }

      bombastic_api_url="$(read_required_secret_key bombastic_api_url)"
      oidc_issuer_url="$(read_required_secret_key oidc_issuer_url)"
      oidc_client_id="$(read_required_secret_key oidc_client_id)"
      oidc_client_secret="$(read_required_secret_key oidc_client_secret)"

      curl_opts=(--silent --show-error --fail-with-body --retry "$HTTP_RETRIES")

      # https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderConfig
      openid_configuration_url="${oidc_issuer_url%/}/.well-known/openid-configuration"
      echo "Getting OIDC issuer configuration from $openid_configuration_url"
      # https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderMetadata
      token_endpoint="$(curl "${curl_opts[@]}" "$openid_configuration_url" | jq -r .token_endpoint)"

      for sbom_path in "${sboms_to_upload[@]}"; do
        original_sbom_relpath="$(realpath "$sbom_path" --relative-base="$SBOMS_DIR")"
        echo
        echo "--- Processing $original_sbom_relpath ---"

        echo "Getting OIDC token from $token_endpoint"
        token_response="$(
          curl "${curl_opts[@]}" \
            -u "${oidc_client_id}:${oidc_client_secret}" \
            -d "grant_type=client_credentials" \
            "$token_endpoint"
        )"
        # https://www.rfc-editor.org/rfc/rfc6749.html#section-5.1
        access_token="$(jq -r .access_token <<< "$token_response")"
        token_type="$(jq -r .token_type <<< "$token_response")"
        expires_in="$(jq -r ".expires_in // empty" <<< "$token_response")"

        retry_max_time=0  # no limit
        if [[ -n "$expires_in" ]]; then
          retry_max_time="$expires_in"
        fi

        # This sbom_id is the one created in the gather-sboms step - sha256:${checksum}
        sbom_id="$(basename -s .json "$sbom_path")"
        supported_version_of_sbom="${sbom_path}.supported_version"

        echo "Uploading SBOM to $bombastic_api_url (with id=$sbom_id)"
        # https://docs.trustification.dev/trustification/user/bombastic.html#publishing-an-sbom-doc
        curl "${curl_opts[@]}" \
          --retry-max-time "$retry_max_time" \
          -H "authorization: $token_type $access_token" \
          -H "transfer-encoding: chunked" \
          -H "content-type: application/json" \
          --data "@$supported_version_of_sbom" \
          "$bombastic_api_url/api/v1/sbom?id=$sbom_id"
      done

    
