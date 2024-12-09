:_mod-docs-content-type: PROCEDURE

[id="post-install"]
= Post-installation integrations

After installing {ProductShortName}, complete the following tasks to ensure that {ProductShortName} works properly.

== Integrating Quay into ACS (Optional)

If you are using your own Quay instance instead of Quay.io, or if you plan to use private repositories in Quay, then you must integrate Quay into ACS. This ensures ACS has access to the repositories you use in Quay.  

.Procedure

. Go to your ACS instance. If you did not have ACS before installing {ProductShortName}, you can find the access details in the `rhtap-cli deploy` command output, which you saved to `~/install_values.txt` at the end of the installation procedure. 

. Follow the instructions in the link:https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_security_for_kubernetes/4.5/html/integrating/integrate-with-image-vulnerability-scanners#integrate-with-qcr-scanner_integrate-with-image-vulnerability-scanners[Red Hat Advanced Cluster Security for Kubernetes 4.5] documentation to integrate Quay into ACS.

== Additional integrations

If you integrated other tools into {ProductShortName}, you must configure them so they can run the build pipelines provided by {ProductShortName}:

[cols="1,1", options="header"]
|===
| If you integrated | Then

| Bitbucket
| Review the link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html/setting_up_bitbucket_for_security_integrations/index[Setting up Bitbucket for security integrations] guide.

| Jenkins
| Review the link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html/setting_up_bitbucket_for_security_integrations/index[Setting up Jenkins for security integrations] guide.

|===



