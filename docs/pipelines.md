Running with gitlab-runner 17.6.0 (374d34fd)
  on ccs-data-projects-runner-b48d9895c-f5vns PaE1vzyU, system ID: r_6UNpmpzjLtCd
Resolving secrets
Preparing the "kubernetes" executor
00:00
Using Kubernetes namespace: opl-ui--pipeline
Using Kubernetes executor with image registry.redhat.io/ubi8/buildah:latest ...
Using attach strategy to execute scripts...
Preparing environment
00:21
Using FF_USE_POD_ACTIVE_DEADLINE_SECONDS, the Pod activeDeadlineSeconds will be set to the job timeout: 1h0m0s...
Waiting for pod opl-ui--pipeline/runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 to be running, status is Pending
Waiting for pod opl-ui--pipeline/runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 to be running, status is Pending
	ContainersNotInitialized: "containers with incomplete status: [init-permissions]"
	ContainersNotReady: "containers with unready status: [build helper]"
	ContainersNotReady: "containers with unready status: [build helper]"
Waiting for pod opl-ui--pipeline/runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 to be running, status is Pending
	ContainersNotReady: "containers with unready status: [build helper]"
	ContainersNotReady: "containers with unready status: [build helper]"
Waiting for pod opl-ui--pipeline/runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 to be running, status is Pending
	ContainersNotReady: "containers with unready status: [build helper]"
	ContainersNotReady: "containers with unready status: [build helper]"
Waiting for pod opl-ui--pipeline/runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 to be running, status is Pending
	ContainersNotReady: "containers with unready status: [build helper]"
	ContainersNotReady: "containers with unready status: [build helper]"
Waiting for pod opl-ui--pipeline/runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 to be running, status is Pending
	ContainersNotReady: "containers with unready status: [build helper]"
	ContainersNotReady: "containers with unready status: [build helper]"
Waiting for pod opl-ui--pipeline/runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 to be running, status is Pending
	ContainersNotReady: "containers with unready status: [build helper]"
	ContainersNotReady: "containers with unready status: [build helper]"
Running on runner-pae1vzyu-project-83725-concurrent-0-kkmeywc1 via ccs-data-projects-runner-b48d9895c-f5vns...
Getting source from Git repository
00:03
Fetching changes with git depth set to 20...
Initialized empty Git repository in /builds/ccs-data-projects/opl-ui/.git/
Created fresh repository.
Checking out e5238e31 as detached HEAD (ref is master)...
Skipping Git submodules setup
Executing "step_script" stage of the job script
00:01
$ if [[ -n ${CI_COMMIT_TAG} ]]; then # collapsed multi-line command
$ buildah --storage-driver=${STORAGE_DRIVER:-vfs} bud ${BUILD_EXTRA_ARGS:-} --format=${IMAGE_FORMAT:-oci} --tls-verify=${TLS_VERIFY:-true} --no-cache -f ${DOCKERFILE:-Dockerfile} -t ${OCI_IMAGE_NAME}:${OCI_IMAGE_TAG:-latest} ${BUILD_CONTEXT:-.}
time="2024-12-04T12:03:15Z" level=warning msg="Reading allowed ID mappings: reading subuid mappings for user \"1004050000\" and subgid mappings for group \"1004050000\": no subuid ranges found for user \"1004050000\" in /etc/subuid"
time="2024-12-04T12:03:15Z" level=warning msg="Found no UID ranges set aside for user \"1004050000\" in /etc/subuid."
time="2024-12-04T12:03:15Z" level=warning msg="Found no GID ranges set aside for user \"1004050000\" in /etc/subgid."
Error during unshare(CLONE_NEWUSER): Function not implemented
time="2024-12-04T12:03:15Z" level=error msg="parsing PID \"\": strconv.Atoi: parsing \"\": invalid syntax"
time="2024-12-04T12:03:15Z" level=error msg="(Unable to determine exit status)"
Cleaning up project directory and file based variables
00:00
ERROR: Job failed: command terminated with exit code 1
