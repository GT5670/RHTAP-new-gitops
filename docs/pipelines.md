:_mod-docs-content-type: PROCEDURE

[id="build-an-application-with-sample-software-templates_{context}"]
= Build an application with sample software templates

{ProductShortName}’s ready-to-use software templates include default integrations with key technologies to further secure and optimize your development experience:

* *ACS (Advanced Cluster Security):* Bolsters your deployments by identifying and mitigating vulnerabilities early in the development process, ensuring your applications are fortified from inception to deployment.

* *Quay:* Acts as a secure harbor for your container images, providing a reliable repository that continuously scans for vulnerabilities, keeping your containerized applications safe.

* *Tekton Pipelines:* Automates your build and deployment processes with precision, enabling a CI/CD framework that integrates seamlessly into your SDLC, thus accelerating your path to production.

* *GitOps:* Implements a GitOps strategy by maintaining your infrastructure and application configurations in Git repositories, ensuring consistent and automated deployment across all environments.

Additionally, {ProductShortName} supports the development and containerization of applications across a wide range of popular programming languages such as Java, Python, Node.js, and Go, expanding your application development capabilities.

Upon the installation of {ProductShortName}, cluster administrators have the capability to tailor the {RHDHLongName} portal with specific templates and enhancements. This customization process is crucial for enabling developers to focus primarily on coding by simplifying development workflows and mitigating concerns related to pipelines, vulnerabilities, and policies.

Before proceeding with customization, it's essential for cluster administrators to familiarize themselves with the available software and pipeline templates through this guide. Such exploration is key to grasping how {ProductShortName} supports a secure supply chain, laying the groundwork for any subsequent customization.

== Setting the stage

* Ensure you have successfully installed {ProductShortName}.

** If you integrated Jenkins during the installation of {ProductShortName}, you must link:https://placeholder.com[configure Jenkins with the appropriate credentials] before using the secure software templates.

** If you integrated Bitbucket while installing {ProductShortName}, ensure the following prerequisites are met, as the secure software templates require them to create a source repository at the correct location:

*** link:https://support.atlassian.com/bitbucket-cloud/docs/create-a-project/[Create a project] in a Bitbucket link:https://support.atlassian.com/bitbucket-cloud/docs/what-is-a-workspace/[workspace].

*** link:https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/[Create an app password] in Bitbucket.

* Log in to {RHDHLongName} ({RHDHShortName}) using the link provided by {ProductShortName} installer at the end of the installation process.

== Build an application

On the {RHDHShortName} portal, select *Create*, and then select an appropriate template. For example, Quarkus Java - Trusted Application Pipeline.

Building an application or microservice for your developers in {RHDHShortName} using the templates offered by {ProductShortName} is essentially only a three step process:

* Provide application information

* Provide application repository information

* Provide deployment information

[discrete]
=== Provide application information

. In the *Name* field, provide an application name. Your name may incorporate lowercase letters (a-z), numbers (0-9), and dashes (-), but it must start and end with a lowercase alphanumeric character. Examples of valid names are `my-name` or `abc-123`, and the length should range from 1 to 63 characters.

. From the *Owner* dropdown list, select an appropriate RHDH component owner for this application. The default value is `user:guest`, which appears if no specific owner is registered in the system. If you have not registered an owner, retain the default `user:guest` selection. If needed, you have the option to replace `guest` with your username, personalizing ownership of the application.

. Select *Next*. The system displays the Application Repository Information form.

[discrete]
=== Provide application repository information

. From the *Host Type* dropdown list, select an appropriate repository host type:

** GitHub

** GitLab

** Bitbucket

. In the *Repository Name* field, enter an appropriate repository name using characters restricted to A-Z, a-z, 0-9, underscore (_), and dashes (-). The system uses this information to name the repository that it creates on the host repository server.

. In the *Repository Owner* field, specify the name of the organization, personal account, or project that Owns the Git repository. For example, this could be the name of your personal user account (username), an organization, or project within organization.

. In the *Repository Server* field, specify the repository server:

+
[cols="1,1", options="header"]
|===
| If you select the Host type | Description

| GitHub
a| The field is pre-populated with `github.com`. However, you can enter your on-prem host URL without the `HTTP` protocol and without the `.git` extension. For example, `github-github.apps.cluster-ljg9z.sandbox219.opentlc.com`.

| GitLab
a| The field is pre-populated with `gitlab.com`. However, you can enter your on-prem host URL without the `HTTP` protocol and without the `.git` extension. For example, `gitlab-gitlab.apps.cluster-ljg9z.sandbox219.opentlc.com`.

| Bitbucket
| The field is pre-populated with `bitbucket.org`.

|===

. In the *Repository Default Branch* field, specify the default branch for your repository. The field defaults to `main`. You can keep it as `main` or specify a different branch name.


. For Bitbucket only:

.. In the *Workspace* field, enter the name of your workspace that contains your project.

.. In the *Project* field, enter project key. The project key is located next to the project name in Bitbucket.

. From the *CI Provider* drop-down list, select the appropriate continuous integration (CI) tool that the system uses to build, test, and deploy the application:

+
[cols="1,1", options="header"]
|===

| For Host type | Available CI providers

| Bitbucket
a|
* Jenkins (SLSA 2)
* Tekton (SLSA 3)

| GitHub
a|
* Jenkins (SLSA 2)
* Github Actions (SLSA 2) (Technical Preview)
* Tekton (SLSA 3)

| GitLab
a|
* Jenkins (SLSA 2)
* Tekton (SLSA 3)
* GitLab CI

|===

+
[IMPORTANT]
====
After you complete creating an application:

* If you select *Bitbucket* as a source repository, you must add Tekton CI webhook in Bitbucket.

* If you select *GitLab CI*, you must add a webhook in GitLab and configure secrets.

* If you select *Jenkins*, you must add your application to Jenkins.
====

. Select *Next*. The system displays the Deployment Information form.

[discrete]
=== Provide deployment information

. In the *Image Registry* field, enter your on-prem image registry URL without the `HTTP` protocol. For example, quay-tv2pb.apps.cluster-tv2pb.sandbox1194.opentlc.com.

. In the *Image Organization* field, enter the image organization for the image registry you provided in the Step 1.

. In the *Image Name* field, enter an appropriate image name following these guidelines: use only lowercase letters, dights, and separators. Separators include a period (.), up to two underscores (_), or one or more hyphens (-). For example, `my-app_1.2`.

+
[NOTE]
====
You must ensure that the name does not start or end with a separator.
====

. In the *Deployment Namespace* field, enter the prefix for the namespaces or cluster where your intend to deploy your application. The system creates the actual namespaces as `rhtap-app-development`, `rhtap-app-stage`, and `rhtap-app-prod`.

+
[NOTE]
====
`rhtap-app` is the default deployment namespace prefix. Cluster administrators have the option to customize this prefix. For instructions on how to customize the default deployment namespace prefix, refer to link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html/customizing_red_hat_trusted_application_pipeline[Customizing sample software templates].
====

. Select *Review* to review all the information that you added.

. Select *Create*.  {ProductShortName} initiates a sequence of automated tasks that are pivotal for setting up your application's infrastructure and deployment pipeline. This process involves several key operations that unfold behind the scenes:

+
* *Repository Creation and Configuration:* A new repository is automatically created in your specified hosting service (GitLab or GitHub), tailored specifically for your application. This includes the setup of both the GitOps repository, which holds your deployment configurations, and the source repository, where your application code resides.

* *Argo CD Integration:* With the repositories in place, Argo CD resources are created and configured. Argo CD, a declarative, GitOps continuous delivery tool, springs into action, orchestrating the deployment of your application across the specified namespaces.

* *Namespace Creation:* As part of setting up your deployment environments, various namespaces are automatically generated based on your application's requirements. This includes separate namespaces for development, staging, and production environments, ensuring isolation and security between stages.

* *Pipeline Definition:* Finally, a pipeline definition is added to your setup, providing you with a 'Pipeline as code' model. This defines the automated workflow for building, testing, and deploying your application, aligning with best practices and security measures.

== Review your application

Once you've successfully created an application using {ProductShortName}, reviewing its components, source code, GitOps configurations, and associated documentation is straightforward. 

*Quick analysis*

For a quick review, click the links that the system displays on the "Run of ..." page. The links provide information for important resources such as:

* Source repositories

* GitOps repositories

*Comprehensive analysis*

For a detailed analysis, follow these steps:

* Select *Open Component in catalog* or you can also navigate to the *Catalog* where the system lists your newly created application.

* *Examine the Source Code:*

+
. Go to the *Overview* tab and select *View Source* to open the repository where your application's source code is housed. This step provides insight into the construction and logic of your application.

* *Review deployment history:*

+
. Go to the *Overview* tab and navigate to the Deployment summary section to review the summary of your application’s deployment across namespaces. Additionally, select an appropriate Argo CD app to open the deployment details in Argo CD, or select a commit ID from the Revision column to review the changes in GitLab or GitHub.

* *Review GitOps repository:*

+
. On the *Overview* tab, use the *Kind* dropdown to select *Resource* and find the relevant GitOps repository.
. Choose *View Source* to examine the GitOps configurations directly. Alternatively, for a broader overview including technical documentation, select *View TechDocs* from the *Catalog* section and then choose the GitOps repository under the *Home* > *Repository* section.


* *Review the Documentation:*

+
. From the *Overview* tab, click *View Tech Docs*.
. This opens the technical documentation for your application, providing detailed insights into its features, configuration steps, and how to utilize it effectively.

== (Optional) Unregister your application

This process removes the application's source and GitOps repository from your catalog and resource view, essentially hiding it. The application itself remains functional within the cluster. Unregistered applications can be re-registered at any time.

. Navigate to the *Catalog* and select the component that you want to unregister.

. Select vertical three-dot menu associated with the component, and then select *Unregister entity*. A confirmation dialog appears.

+
image::unregister.png[]

. Select *Unregister Location*. This removes the application's Git repository from your catalog view.

. Navigate to the *Catalog*, from the *Kind* drop down list, select *Resource*, and then unregister the corresponding GitOps resource.

. Remove the application from the cluster, by running the following command:

+
[source,bash]
----
oc delete application your-app-name-app-of-apps -n rhtap # <1>
----
<1> `rhtap` is the default namespace. Additionally, `your-app-name` is the name of your application.

[role="_additional-resources"]
.Next steps

* If you selected Bitbucket as repository host, see link:https://placeholder.com[Setting up Bitbucket for Security Integrations]

* If you selected Jenkins CI, see link:https://placeholder.com[Add your application to Jenkins]

* If you selected GitLab CI, see link:https://placeholder.com[Setting up GitLab for Security Integrations]

* xref:update-code-and-view-security-insights_{context}[Update code and view security insights]
