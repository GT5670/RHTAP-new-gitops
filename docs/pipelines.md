:_mod-docs-content-type: PROCEDURE

[id="configuring-rhtap-to-use-built-in-jenkins-libraries_{context}"]
= Configuring {ProductShortName} to use built-in Jenkins libraries

By default {ProductLongName} ({ProductShortName}) uses dynamically loaded Jenkins libraries. While dynamically loading provides flexibility, using built-in Jenkins libraries offer improved stability, security, and traceability during builds. Configuring {ProductShortName} to use built-in libraries instead of dynamically loaded ones allows for better {ECLong} ({ECShort}) attestations and enhanced build verification.

.Prerequisites

* You must have administrator access to the Jenkins instance in {ProductShortName}.

* You must have the Jenkins library git repo URL. For example, `https://github.com/redhat-appstudio/tssc-sample-jenkins`. You can find the Git repository URL in the default link:https://github.com/redhat-appstudio/tssc-sample-templates/blob/main/skeleton/ci/source-repo/jenkins/Jenkinsfile[{ProductShortName} Jenkins CI source repository].

* You must have permissions to modify the `Jenkinsfile`.

== Define the built-in library in Jenkins

.Procedure

. Log in to Jenkins and navigate to *Manage Jenkins > System*.

. Locate the *Global Trusted Pipeline Libraries* section.

. Click Add and define the new library with the following parameters:

.. *Name*: <your-library-name>

.. *Default version*: Set to a specific branch or commit reference. For example, v{ProductRelease}.

.. *Allow default version to be overridden*: (Optional) Select this if you want to restrict users to a specific version of the Jenkins library. This ensures that the users cannot select a different version.

.. *Include @Library changes in your recent changes*: Select this if you want if you want to track changes made to the shared library. This feature help users understand modifications that might affect their builds.

.. *Retrieval method*: Select *Modern SCM*.

... From the *Source Code Management* drop-down list, select *Git*.

... In the Project Repository field, enter the Jenkins library URL. For example, `https://github.com/redhat-appstudio/tssc-sample-jenkins`.

... Select *Fresh clone per build*, to ensure each build fetches a clean copy of the library.

... Select *Save*.

== Modify the Jenkins pipeline to use the built-in library

.Procedure

. Navigate to your Jenkins CI source repository, For example, https://github.com/redhat-appstudio/tssc-sample-templates/blob/main/skeleton/ci/source-repo/jenkins.

. Select `Jenkinsfile` in edit mode.

. Replace the dynamic library loading with the @Library annotation.

+
[cols="1,1"]
|===
|Replace this | With this

| 
library identifier: 'RHTAP_Jenkins@main', retriever: modernSCM(
  [$class: 'GitSCMSource',
   remote: 'https://github.com/redhat-appstudio/tssc-sample-jenkins.git'])

|@Library('RHTAP_Jenkins@v{ProductRelease}') _
|===

. Save and commit the updated Jenkinsfile.

== Use the configured Jenkins library

.Procedure

. In your Jenkins instance, navigate to your project.

. Select *Build Now* to trigger a new build.

.Verification

. Check the Jenkins build logs to confirm that the built-in library is loaded instead of dynamically retrieving dependencies.

. Validate that {ECShort} attestations now reflect the use of a built-in library.

. If any errors occur, verify the library name, retrieval method, and pipeline script.

== Applying changes to one or all {ProductShortName} templates
Depending on your use case, you can apply this configuration to one {ProductShortName} template or all {ProductShortName} templates in {RHDHLongName} ({RHDHShortname}).

*To apply this change to a single template:*
Modify only the specific pipeline template used in your project. This ensures that only this pipeline uses the built-in Jenkins library, while others continue using dynamic loading.

*To apply this change to all {ProductShortName} templates in {RHDHShortname}:*
Update the global {ProductShortName} template configuration to reference the built-in library instead of dynamically loaded ones. This ensures consistency across all {ProductShortName} pipelines.

[IMPORTANT]

====
Applying this change globally may impact all builds using {ProductShortName}. Ensure that the built-in library is correctly defined and tested before making this change across all templates.
====

