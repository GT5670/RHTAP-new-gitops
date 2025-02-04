:_mod-docs-content-type: PROCEDURE

[id="configuring-rhtap-to-use-built-in-jenkins-libraries_{context}"]
= Configuring {ProductShortName} to use built-in Jenkins libraries

By default {ProductLongname} ({ProductShortName}) uses dynamically loaded Jenkins libraries. While dynamically loading provides flexibility, using built-in Jenkins libraries offer improved stability, security, and traceability during builds. Configuring {ProductShortName} to use built-in libraries instead of dynamically loaded ones allows for better {ECLong} ({ECShort}) attestations and enhanced build verification.

.Prerequisites

* You must have administrator access to the Jenkins instance in {ProductShortName}.

* You must have the Jenkins library git repo URL. For example, https://github.com/redhat-appstudio/tssc-sample-jenkins. You would find the git repo URL in the default link:https://github.com/redhat-appstudio/tssc-sample-templates/blob/main/skeleton/ci/source-repo/jenkins/Jenkinsfile[{ProductShortName} Jenkins CI source repository].

* You must have rights to modify the `Jenkinsfile`.

== Define the built-in library in Jenkins

.Procedure

. Navigate to *Manage Jenkins > System*.

. Locate the *Global Trusted Pipeline Libraries* section.

. Click Add and define the new library with the following parameters:

.. Name: <your-library-name>

.. Default version: Set to a specific branch or commit reference. For example, v{ProductRelease}.

.. Allow default version to be overridden: (Optional) Select this if you really want to lock it down allowing the version to be overridden so that the users would only use your Jenkins at your version without being allowed to pick a new version.

.. Include @Library changes in your recent changes: Select this if you want to see what has changed it'll show you what's changed since last time. So if you do a built and users are using the shared libraries and the libary changed a lot of users may want to know why my built didn't worked like before so when they got to logs and can find what has changes since last time.

.. Retrieval method: Select *Modern SCM*.

... From the *Source Code Management* drop-down list, select *Git*.

... In the Project Repository field, enter the Jenkins library URL. For example, `https://github.com/redhat-appstudio/tssc-sample-jenkins`.

... Select *Fresh clone per build*, to ensure you get clean and don't actually use old stuff.

... Select *Save*.

== Modify the Jenkins pipeline to use the built-in library

.Procedure

. Navigate to your Jenkins CI source repository, For example, https://github.com/redhat-appstudio/tssc-sample-templates/blob/main/skeleton/ci/source-repo/jenkins.

. Select `Jenkinsfile` to open it in the editable format.

. Replace the dynamic library loading with the @Library annotation.

+
[cols="1,1"]
|===
|Replace this | With this

| `library identifier: 'RHTAP_Jenkins@main', retriever: modernSCM(
  [$class: 'GitSCMSource',
   remote: 'https://github.com/redhat-appstudio/tssc-sample-jenkins.git'`

| @Library('RHTAP_Jenkins@v{ProductRelease}') _
|===
