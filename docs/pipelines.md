:_mod-docs-content-type: PROCEDURE

[id="integrating-products-and-external-services_{context}"]
= Integrating products and external services

The {ProductShortName} installer deploys a network of products that work together to form a secure, automated CI/CD platform. However, two of these products you may have already installed: Advanced Cluster Security (ACS) and Quay. If you already have instances of either of these products, you can integrate them into your installation of {ProductShortName}. Integration saves time and prevents data loss. If you have instances of these products and do _not_ integrate them, then the installer just creates new instances in new namespaces.

Additionally, there are three products that you can replace with certain substitutes in your deployment of {ProductShortName}. The table below names these products, their purpose, and what other products you can use instead.

[cols="1,1, 1"]
|===
|Product |Purpose |Possible substitutes

|GitHub
a|Source code repository

a|* GitLab
* Bitbucket

|Tekton
a|CI pipeline

a|* Jenkins
* GitHub Actions
* GitLab CI

CI pipeline substitutes conform to link:https://slsa.dev/spec/v1.0/levels[SLSA] Build L2. Only Tekton conforms to Build L3.

|Quay
a|Registry for artifacts

a|Artifactory

|===

Please note that when you use alternative providers for your Git, CI and registry integrations, {ProductShortName} also installs plugins for those products in {RHDHLongName}. Most of them are Technology Preview or community plugins. This means that *replacing default products can introduce security risks and is not recommended for a production environment.* For more information, please see the plugins table in our link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html/release_notes_for_red_hat_trusted_application_pipeline_{ProductVersion}/con_support-matrix_default[release notes] and the link:https://docs.redhat.com/en/documentation/red_hat_developer_hub/{RHDHVersion}/html/dynamic_plugins_reference/con-preinstalled-dynamic-plugins#snip-dynamic-plugins-support_title-plugins-rhdh-about[{RHDHShortName} documentation] about plugins.  

Also be aware that, to customize your installation, you must run all relevant commands inside an `rhtap-cli` container, which is logged into your cluster as ClusterAdmin.

The following procedures explain how to customize your installation of {ProductShortName}, by integrating pre-existing instances and outside products.
