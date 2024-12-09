:_mod-docs-content-type: PROCEDURE

[id="post-install"]
= Post-installation integrations

After installing {ProductShortName}, there are a several scenarios that require you to complete some additional work, to ensure {ProductShortName} functions properly.

== (Optional) Integrating Quay into ACS

Again, if you are using your own instance of Quay, instead of Quay.io, or if you plan to use private repositories in Quay, you must ensure ACS can access your images.

If you integrated your own instance of Quay into {ProductShortName}, or if you want to use private repositories in Quay, then you must now integrate Quay into ACS. This ensures ACS has access to the repositories you use in Quay.  

.Procedure

. Go to your instance of ACS. If you did not have ACS prior to installation, then the details you need for access were given in the output of the `rhtap-cli deploy` command. You saved this output in `~/install_values.txt`, near the end of the installation procedure. 

. Follow the instructions in link:https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_security_for_kubernetes/4.5/html/integrating/integrate-with-image-vulnerability-scanners#integrate-with-qcr-scanner_integrate-with-image-vulnerability-scanners[this document] to integrate Quay into ACS.

If you integrated Jenkins into {ProductShortName}, configure Jenkins using the Jenkins UI to ensure it can run the build pipelines provided by {ProductShortName}. To configure Jenkins, see [url]

Additionally, if you integrated GitLab into {ProductShortName}, configure GitLab to ensure it can run the build pipelines provided by {ProductShortName}. To configure GitLab, see [url]

If you integrated Bitkucket into {ProductShortName}, configure Bitbucket to ensure it can run the build pipelines provided by {ProductShortName}. To configure Bitbucvket, see [url]
