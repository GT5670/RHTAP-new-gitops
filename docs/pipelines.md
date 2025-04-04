:_mod-docs-content-type: PROCEDURE
:azure: 

[id="adding-secrets-to-azure-pipeline-for-secure-integration-with-external-tools_{context}"]
= Adding secrets to Azure Pipeline for secure integration with external tools

.Prerequisites

Before you configure Azure Pipeline, ensure you have the following:

* *Admin* access to your repository in Bitbucket, GitHub, and GitLab.

* *Admin* access to your Azure pipeline settings.

* *Container registry credentials* for pulling container images from Quay.io, JFrog Artifactory, or Sonatype Nexus.

* *Authentication details* for specific Azure Pipeline tasks:

** *For ACS security tasks*:

*** ROX Central server endpoint
*** ROX API token

** *For SBOM and artifact signing tasks*:

*** Cosign signing key password
*** Private key and public key
*** Trustification URL
*** Client ID and secret
*** Supported CycloneDX version

+
[NOTE]
====
The credentials and other details are already Base64-encoded, so you do not need to encode them again. You can find these credentials in your `private.env` file, which you created during {ProductShortName} installation. 
====

.Procedure 

== Option 1: Using Azure UI

. Log in to Azure and open your Azure DevOps project.

. In the left navigation panel, click *Pipelines*, and then click *Library*.

. Click **+ Variable group** to create a new variable group.

. Enter a name for the variable group, for example, `azure-pipeline-secrets`.

. In the variable group editor:

.. Click **+ Add** to add a new variable.

.. In the **Name** field, enter the key, for example, `MY_GITLAB_TOKEN`.

.. In the *Value* field, enter the link:https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html#create-a-personal-access-token[token] associated with your GitLab account.

.. Select the **Keep this value secret** checkbox to mask the value.

. Repeat steps 3-4 to add the required variables:

+
include::../snippets/gitlab_github_variables/ui_variables.adoc[]


. Click **Save**.

. To authorize pipelines to use the variable group:
.. Click the **Pipeline permissions** tab in the same view.

.. Click **+ Add pipeline**.

.. Select the pipelines that require access to this variable group.

. In your pipeline YAML file, include the variable group:
+
[source,yaml]
----
variables:
- group: azure-pipeline-secrets
----

. Reference the variables in your steps using Azure DevOps syntax. For example:
+
[source,yaml]
----
steps:
- script: echo "Using GitLab token"
  env:
    GITLAB_TOKEN: $(GITLAB_TOKEN)
----

. Rerun the last pipeline run to verify the secrets are applied correctly.

. Alternatively, switch to your application's source repository in Azure DevOps, make a minor change, and commit it to trigger a new pipeline run.
