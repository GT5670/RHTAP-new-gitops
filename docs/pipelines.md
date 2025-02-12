:_mod-docs-content-type: PROCEDURE

[id="customizing-sample-software-templates_{context}"]
= Customizing sample software templates

Learn how to customize ready-to-use software templates for your on-prem environment. Cluster administrators have full control over this process, including modifying metadata and specifications.

.Prerequisites

* You have used the forked repository URL from link:https://github.com/redhat-appstudio/tssc-sample-templates[tssc-sample-templates] during the {ProductShortName} install process.

* You have already forked and cloned the https://github.com/redhat-appstudio/tssc-sample-jenkins.git[tssc-sample-jenkins] pipeline template.

* You must ensure your forked version is up to date and in sync with the upstream repository.

.Procedure

. Clone your forked `tssc-sample-templates` repository, and then open it in your preferred text editor, such as Visual Studio Code.

. Locate the *properties* file within your project directory. This file stores the default values that you can customize. Open it for editing and update the following key-value pairs according to your environment.

+
[cols="1,1"]
|===
|Key |Description

|export GITHUB_DEFAULT_HOST
a|Set this to your on-prem GitHub host fully qualified domain name. That is, the URL without the `HTTP` protocol and without the `.git` extension. For example github-github.apps.cluster-ljg9z.sandbox219.opentlc.com. Default is `github.com`. 

|export GITLAB_DEFAULT_HOST
a|Set this to your on-prem GitLab host host fully qualified domain name. That is, the URL without the `HTTP` protocol and without the `.git` extension. For example gitlab-gitlab.apps.cluster-ljg9z.sandbox219.opentlc.com. Default is `gitlab.com`.

|export QUAY_DEFAULT_HOST
a|The default Quay URL corresponds to your specific on-prem image registry URL without the `HTTP` protocol. For example, quay-tv2pb.apps.cluster-tv2pb.sandbox1194.opentlc.com. The default quay host is `quay.io`.

|export DEFAULT_DEPLOYMENT_NAMESPACE_PREFIX
a|The namespace prefix for deployments within {ProductShortName}. Default is `rhtap-app`.

NOTE: Update this if you have modified the default `trusted-application-pipeline: namespace` during the {ProductShortName} installation process.

|export PIPELINE_REPO_URL
a|The URL of the forked pipeline repository. For example,  https://github.com/redhat-appstudio/tssc-sample-pipelines.

|export PIPELINE_REPO_BRANCH
a|The branch of the forked pipeline repository to which you want to point. For example, `main`.

|export GITHUB_DEFAULT_ORG
a|The name of your GitHub organization that you want to set as default.

|export QUAY_DEFAULT_ORG
a|The name of your Quay organization that you want to set as default.

|===

+
.The properties file
image::properties.png[]

. Run the *generate.sh* script in your terminal. This action adjusts the software templates, replacing default host values with your specified inputs.

+
[source,terminal]
----
./generate.sh
----

+
.The generate.sh script
image::generate.png[]

. For Jenkins only: To customize your Jenkins library, navigate to *skeleton > ci > gitops-template > jenkins*, and open *Jenkinsfile*. Replace the `remote` URL with the URL of your forked repository. For example, remote: 'https://github.com/<username>/tssc-sample-jenkins.git'.
+
[[rekor-tuf-note]]
Additionally, if your Jenkins is on a non-local OpenShift instance, and your Rekor and TUF services are on different clusters, update the `REKOR_HOST` and `TUF_MIRROR` environment variables. You can configure these variables in the *env.sh* file within the component repository or set them as link:https://docs.redhat.com/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html/configuring_jenkins/configuring-jenkins-with-the-appropriate-credentials_jenkins[environment variables or secrets in Jenkins]. This configuration ensures that your external Jenkins server can communicate with Rekor and TUF installed with {ProductShortName}. Without this, {ProductShortName} might not sign container images correctly in the Jenkins pipeline.
+
To update the `REKOR_HOST` and `TUF_MIRROR` variables:
+
.. Open the *env.sh* file via *skeleton > ci > gitops-template > jenkins > rhtap*.
+
The second *env.sh* file is located at *skeleton > ci > source-repo > jenkins > rhtap*. Pick the one that suits your needs or update both.
+
In *env.sh*, review the default values for `REKOR_HOST` and `TUF_MIRROR`:
+
----
REKOR_HOST=http://rekor-server.rhtap-tas.svc
TUF_MIRROR=http://tuf.rhtap-tas.svc
----
+
.. Replace `.svc` with your OpenShift cluster URL. The `.svc` domain refers to the local cluster, and internal services can access other services with `.svc` in their routes, but an external Jenkins cannot. 
+
The correct routes of the Rekor and TUF services are printed as part of the installation process of {ProductShortName}. If these data aren’t available to you, run this command in your CLI and select the Rekor and TUF routes in the output: 
+
----
$ oc get routes -n rhtap-tas
----
+
An example of a Rekor server URL: \http://rekor-server.rhtap-tas.apps.rosa.j6ufg-t3htv-ts6.z797.p3.openshiftapps.com.

+
[NOTE]
====

* To configure environment variables or secrets in Jenkins see, link:https://docs.redhat.com/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html/configuring_jenkins/configuring-jenkins-with-the-appropriate-credentials_jenkins[Adding secrets to Jenkins for secure integration with external tools].

* By default, {ProductShortName} uses dynamically loaded Jenkins libraries. If you need to configure {ProductShortName} to use built-in Jenkins libraries instead of dynamic loading, you must modify the Jenkins provisioning setup. This change can improve traceability and {ECLong} ({ECShort}) attestations. For detailed instructions, see xref:configuring-rhtap-to-use-built-in-jenkins-libraries_{context}[Configuring {ProductShortName} to use built-in Jenkins libraries].
====

. For RHACS only: To enable RHACS scans, set the `export DISABLE_ACS` to `false` in the *env.sh* file.

. Commit and push the changes to your repository. This automatically updates the template in {RHDHShortName}. Alternatively, you can import and refresh a single or all customized templates directly in {RHDHShortName}.

.. Go to your forked sample template repository on your Git provider.

.. For a single template, from the `templates` directory, select `template.yaml`. Copy its URL from the browser address bar. For example, \https://github.com/<username>/tssc-sample-templates/blob/main/templates/devfile-sample-code-with-quarkus-dance/template.yaml. Otherwise, for all the templates, select `all.yaml` and copy its URL from the browser address bar. For example, \https://github.com/<username>/tssc-sample-templates/blob/main/all.yaml.

.. Switch back to {RHDHShortName} platform.

.. Select *Create* > *Register Existing Component*.

.. In the *Select URL* field, paste the appropriate URL that you copied in Step 4b.

.. Select *Analyze* and then select *Import* to update the templates in {RHDHShortName}.

.Verification

* Consider creating an application to explore the impact of your template customization.

[role="_additional-resources"]
.Additional resources

* To customize pipelines, see xref:customizing-sample-pipelines_{context}[Customizing sample pipeline templates]
