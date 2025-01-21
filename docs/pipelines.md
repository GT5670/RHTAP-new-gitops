gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ sudo systemctl start docker
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ sudo systemctl enable docker
Created symlink '/etc/systemd/system/multi-user.target.wants/docker.service' → '/usr/lib/systemd/system/docker.service'.
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker --version
Docker version 27.3.1, build 2.fc41
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker login quay.io
Username: rhdeveldocs
Password: 
WARNING! Your password will be stored unencrypted in /home/gtrivedi/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credential-stores

Login Succeeded
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker pull quay.io/coreos/etcd
Using default tag: latest
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/images/create?fromImage=quay.io%2Fcoreos%2Fetcd&tag=latest": dial unix /var/run/docker.sock: connect: permission denied
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker pull ubuntu:latest
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/images/create?fromImage=ubuntu&tag=latest": dial unix /var/run/docker.sock: connect: permission denied
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ getent group docker
docker:x:971:
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ sudo usermod -aG docker $USER
[sudo] password for gtrivedi: 
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ newgrp docker
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete 
Digest: sha256:1b7a37f2a0e26e55ba2916e0c53bfbe60d9bd43e390e31aacd25cb3581ed74e6
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ sudo systemctl enable docker
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ sudo systemctl start docker
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ sudo systemctl status docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: disabled)
    Drop-In: /usr/lib/systemd/system/service.d
             └─10-timeout-abort.conf, 50-keep-warm.conf
     Active: active (running) since Tue 2025-01-21 20:46:57 IST; 9min ago
 Invocation: 9d72a46053f8406b9571d09471e86bf2
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 161697 (dockerd)
      Tasks: 25
     Memory: 70.9M (peak: 73.5M)
        CPU: 526ms
     CGroup: /system.slice/docker.service
             └─161697 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --selinux-enabled --userland-proxy-path /usr/bin/docker-proxy --init-path /usr>

Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.214397680+05:30" level=info msg="Firewalld: created docker-forwarding policy"
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.688066061+05:30" level=info msg="Firewalld: interface docker0 already part o>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.791586207+05:30" level=info msg="Loading containers: done."
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.808996788+05:30" level=warning msg="WARNING: bridge-nf-call-iptables is disa>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.809131020+05:30" level=warning msg="WARNING: bridge-nf-call-ip6tables is dis>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.809160936+05:30" level=info msg="Docker daemon" commit=2.fc41 containerd-sna>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.809322609+05:30" level=info msg="Daemon has completed initialization"
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.869233273+05:30" level=info msg="API listen on /run/docker.sock"
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb systemd[1]: Started docker.service - Docker Application Container Engine.
Jan 21 20:55:24 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:55:24.167308590+05:30" level=info msg="ignoring event" container=95dd89fd7baff5033>
...skipping...
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: disabled)
    Drop-In: /usr/lib/systemd/system/service.d
             └─10-timeout-abort.conf, 50-keep-warm.conf
     Active: active (running) since Tue 2025-01-21 20:46:57 IST; 9min ago
 Invocation: 9d72a46053f8406b9571d09471e86bf2
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 161697 (dockerd)
      Tasks: 25
     Memory: 70.9M (peak: 73.5M)
        CPU: 526ms
     CGroup: /system.slice/docker.service
             └─161697 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --selinux-enabled --userland-proxy-path /usr/bin/docker-proxy --init-path /usr>

Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.214397680+05:30" level=info msg="Firewalld: created docker-forwarding policy"
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.688066061+05:30" level=info msg="Firewalld: interface docker0 already part o>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.791586207+05:30" level=info msg="Loading containers: done."
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.808996788+05:30" level=warning msg="WARNING: bridge-nf-call-iptables is disa>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.809131020+05:30" level=warning msg="WARNING: bridge-nf-call-ip6tables is dis>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.809160936+05:30" level=info msg="Docker daemon" commit=2.fc41 containerd-sna>
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.809322609+05:30" level=info msg="Daemon has completed initialization"
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:46:57.869233273+05:30" level=info msg="API listen on /run/docker.sock"
Jan 21 20:46:57 gtrivedi-thinkpadp16vgen1.rmtin.csb systemd[1]: Started docker.service - Docker Application Container Engine.
Jan 21 20:55:24 gtrivedi-thinkpadp16vgen1.rmtin.csb dockerd[161697]: time="2025-01-21T20:55:24.167308590+05:30" level=info msg="ignoring event" container=95dd89fd7baff5033>
~
~
~
~
~
~
~
~
~
~
~
~
~
~
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker pull quay.io/coreos/etcd
Using default tag: latest
latest: Pulling from coreos/etcd
[DEPRECATION NOTICE] Docker Image Format v1 and Docker Image manifest version 2, schema 1 support is disabled by default and will be removed in an upcoming release. Suggest the author of quay.io/coreos/etcd:latest to upgrade the image to the OCI Format or Docker Image manifest v2, schema 2. More information at https://docs.docker.com/go/deprecated-image-specs/
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker pull ubuntu:latest
latest: Pulling from library/ubuntu
de44b265507a: Pull complete 
Digest: sha256:80dd3c3b9c6cecb9f1667e9290b3bc61b78c2678c02cbdae5f0fea92cc6734ab
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker tag ubuntu:latest quay.io/rhdeveldocs/ubuntu:latest
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/rhtap$ docker push quay.io/rhdeveldocs/ubuntu:latest
