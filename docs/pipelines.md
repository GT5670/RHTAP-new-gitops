= Installing {ProductName}

{ProductName} ({ProductShortName}) is not really a single product. Instead, it is a set of products that combine to form a highly automated, customizable, and secure platform for building applications.

By default, {ProductShortName} includes the following products:

* link:https://docs.redhat.com/documentation/red_hat_advanced_cluster_security_for_kubernetes/{ACSVersion}/[Advanced Cluster Security (ACS)]: to scan your artifacts for vulnerabilities.

* link:https://docs.redhat.com/documentation/red_hat_developer_hub/{RHDHVersion}[Developer Hub]: a self-service portal, to consolidate management of applications across their lifecycle.

* link:https://next.redhat.com/2023/06/13/introducing-enterprise-contract/[Enterprise Contract]: to validate your artifacts against customizable policies.

* link:https://docs.redhat.com/documentation/red_hat_openshift_gitops/{OSGitOpsVersion}/[OpenShift GitOps]: to manage Kubernetes deployments and their infrastructure.

* link:https://docs.redhat.com/documentation/red_hat_openshift_pipelines/{OSPipelinesVersion}/[OpenShift Pipelines]: to enable automation and provide visibility for continuous integration and continuous delivery (CI/CD) of software.

* link:https://docs.redhat.com/documentation/red_hat_quay/{QuayVersion}[Quay.io]: a container registry, to store your artifacts.

* link:https://docs.redhat.com/documentation/en-us/red_hat_trusted_artifact_signer/{RHTASVersion}[Trusted Artifact Signer]: to sign and validate the artifacts that {ProductShortName} produces.

* link:https://docs.redhat.com/documentation/red_hat_trusted_profile_analyzer/{RHTPAVersion}[Trusted Profile Analyzer]: to deliver actionable information about your security posture.

You can see exactly which versions of these products {ProductShortName} supports in the compatibility and support matrix of our link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html/release_notes_for_red_hat_trusted_application_pipeline_{ProductVersion}/con_support-matrix_default[Release notes].

NOTE: {ProductName} supports many alternatives to this default combination of products. Later in the installation process, this documentation explains how to customize your deployment to meet your needs.  

Because a fully-operational instance of {ProductShortName} involves all of the products listed above, installing {ProductShortName} takes some effort. However, we have automated the vast majority of this process with an installer tool packaged as a container image.

Be aware that the {ProductShortName} installer is not a manager: it does not support upgrades. The installer generates your first deployment of {ProductShortName}. But after installation, you must manage each product within {ProductShortName} separately. And while the installer can be run multiple times, doing so after manually changing the configuration of a product may have unpredictable results.

Additionally, the products that the installer deploys are production ready, but they are sized for a proof of concept or a very small team. For larger teams, manual reconfiguration of the products is most likely necessary and should be done by following procedures documented for each individual product.

Lastly, please be aware that the {ProductShortName} subscription only includes {RHDHLongName}, {RHTASLongName}, {RHTPALongName}, and {ECLong}. The {ProductShortName} installer deploys all the other products listed above, too. But to use them, you must purchase a subscription for OpenShift Plus.

.Installation steps
To install {ProductShortName} using the installer, you must complete the following procedures.

. Configuring GitHub for {ProductShortName}

. (Optional) Customizing your installation 

. Installing {ProductShortName} in your cluster

. (Optional) Completing integrations after installation

The following pages of this document explain each of those installation steps in detail. 

include::topics/installer-topics/proc_login-and-download-the-image-registry.adoc[leveloffset=+1]

include::topics/installer-topics/proc_creating-the-config-file.adoc[leveloffset=+1]

include::topics/installer-topics/proc_integrating-products-and-external-services.adoc[leveloffset=+1]

include::topics/installer-topics/proc_integrating-github.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-acs.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-quay.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-bitbucket.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-github-actions.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-gitlab.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-jenkins.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-azure-pipelines.adoc[leveloffset=+2]

include::topics/installer-topics/proc_integrating-jfrog-artifactory.adoc[leveloffset=+2]

include::topics/installer-topics/proc_customizing-the-config-file.adoc[leveloffset=+1]

include::topics/installer-topics/proc_deploying-rhtap.adoc[leveloffset=+1]
