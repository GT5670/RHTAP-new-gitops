:_mod-docs-content-type: PROCEDURE

[id="customizing-sample-pipelines_{context}"]
= Customizing sample pipelines

Learn how to update Pipeline as Code (`pac`) URLs within the sample templates repository and to customize the sample pipelines repository to your workflow. By customizing `pac` URLs, organizations can leverage specific pipelines tailored to their needs.

.Prerequisites

* You have already forked and cloned the following templates locally:

** link:https://github.com/redhat-appstudio/tssc-sample-pipelines[Sample pipelines]

** link:https://github.com/redhat-appstudio/tssc-sample-templates[Sample templates]

* You must ensure your forked version is up to date and in sync with the upstream repository.


[discrete]
== Customizing the sample templates repository to update `pac` URLs*

.Procedure

. Access forked sample pipelines repository URL:

.. Open your forked sample pipelines repository.

.. Copy the complete URL from the address bar. For example, https://github.com/<username>/tssc-sample-pipelines.

. Update `pac` URLs in the sample templates repository:

.. Navigate to your local cloned sample templates repository using your terminal.

.. Run the following command, replacing {fork_url} with the copied URL from step 1 and {branch_name} with your desired branch name (for example, main):

+
[source,bash]
----
./scripts/update-tekton-definition {fork_url} {branch_name}

# For example, .scripts/update-tekton-definition https://github.com/<username>/tssc-sample-pipelines main
----

. Review, commit, and push changes:

.. Review the updated files within your sample templates repository.

.. Commit the changes with appropriate message.

.. Push the committed changes to your forked repository.


[discrete]
== Customizing the sample pipelines repository to your workflow

The sample pipelines repository provides a foundation upon which you can build your organization's specific CI/CD workflows. The sample pipelines repository includes several key pipeline templates in the `pac` directory:

* *`gitops-repo`:* This directory holds the pipeline definitions for validating pull requests within your GitOps repository. It triggers the `gitops-pull-request` pipeline, located in the `pipelines` directory, validating that image updates comply with organizational standards. This setup is crucial for promotion workflows, where an application's deployment state is advanced sequentially through environments, such as from development to staging or from staging to production. For more information about pipeline definitions in `gitops-repo`, refer link:https://github.com/redhat-appstudio/tssc-sample-pipelines/blob/main/pac/gitops-repo/README.md[Gitops Pipelines].

* *`pipelines`:* This directory houses the implementations of build and validation pipelines that are referenced by the event handlers in both the `gitops-repo` and `source-repo`. By examining the contents of this directory, you can understand the specific actions performed by the pipelines, including how they contribute to the secure promotion and deployment of applications.

* *`source-repo`*: This directory focuses on Dockerfile-based secure supply chain software builds. It includes pipeline definitions for cloning the source, generating and signing artifacts (such as `.sig` for image signature, `.att` for attestation, and `.sbom` for Software Bill of Materials), and pushing these to the user's image registry. For more information about pipeline definitions in `source-repo`, refer link:https://github.com/redhat-appstudio/tssc-sample-pipelines/blob/main/pac/source-repo/README.md[Shared Git resolver model for shared pipeline and tasks].

* *`tasks`:* This directory houses a collection of tasks that can be added or modified, aligning with organizational needs. For example, Advanced Cluster Security (ACS) tasks can be substituted with alternative checks, or entirely new tasks can be integrated into the pipeline to enhance its functionality and compliance.

.Verification

* Consider creating an application to explore the impact of your template and pipeline customization.

[role="_additional-resources"]
.Additional resources

* To customize templates, see xref:customizing-sample-software-templates_{context}[Customizing sample software templates]

* For information on Pipeline as code, refer link:https://docs.redhat.com/documentation/red_hat_openshift_pipelines/{OSPipelinesVersion}/html/pipelines_as_code/about-pipelines-as-code[About Pipelines as Code].
