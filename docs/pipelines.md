:_mod-docs-content-type: PROCEDURE

[id="login-and-download-the-image-registry_{context}"]
= Log in to Podman and download the installer image

Use this procedure to authenticate with `registry.redhat.io`, download the RHTAP installer image, and launch the installer container. This step is essential because the installer CLI (`rhtap-cli`) runs inside a container and automates the deployment and integration of Red Hat Trusted Application Pipeline (RHTAP) components.

This setup helps you securely configure your environment before starting the installation process.

.Prerequisites

* A container engine installed on your workstation, such as link:https://podman.io/docs/installation[Podman] or link:https://docs.docker.com/get-started/get-docker/[Docker].
* Valid Red Hat credentials for accessing `registry.redhat.io`.

.Procedure

. Log in to the Red Hat registry.
+
[source,bash]
----
podman login registry.redhat.io
----

. Pull the installer image.
+
[source,bash]
----
podman pull registry.redhat.io/rhtap-cli/rhtap-cli-rhel9:latest
----

. Start the installer container.
+
[source,bash]
----
podman run \
  -it \
  --entrypoint bash \ <1>
  --env-file tmp/private.env \ <2>
  --publish 8228:8228 \ <3>
  --rm \
  rhtap-cli:latest <4>
----
<1> Starts the container with a bash shell so that you can interact with it.
<2> Uses an environment file (`private.env`) to securely inject credentials and configuration without exposing them on the CLI.
<3> Exposes port 8228 because the GitHub App creation process runs a temporary local service on this port.
<4> Refers to the installer image that you pulled in the previous step.
