:_mod-docs-content-type: PROCEDURE

[id="creating-the-config-file_{context}"]
= Creating the {ProductShortName} `config.yaml` file

Use this procedure to create the `config.yaml` file. This file defines how Red Hat Trusted Application Pipeline (RHTAP) is deployed in your cluster. It also enables RHTAP to detect any external integrations that you configure during installation.

.Prerequisites

* `cluster-admin` access to your OpenShift Container Platform (OCP) cluster.
* An active `rhtap-cli` container session.

.Procedure

. In the container shell, log in to your OpenShift cluster as a cluster administrator.
+
[source,bash]
----
bash-5.1$ oc login https://api.<your-cluster-domain>:6443 \
  --username=cluster-admin \
  --password=<your-password>
----

. Create the default configuration file for RHTAP.
+
[source,bash]
----
bash-5.1$ rhtap-cli config --create
----

[NOTE]
====
This command creates a configuration map (`config.yaml`) that defines the components {ProductShortName} installs and enables integration support for any pre-existing products. You can customize this file later to suit your environment.
====
