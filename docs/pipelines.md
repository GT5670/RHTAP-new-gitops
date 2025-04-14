:_mod-docs-content-type: PROCEDURE

[id="login-and-download-the-image-registry_{context}"]
= Login to podman and download the image registry

Write a short introductory paragraph that provides an overview of the module. The introduction should include what the module will help the user do and why it will be beneficial to the user. Include key words that relate to the module to maximize search engine optimization.

.Prerequisites

* A container management tool on your workstation, such as link:https://podman.io/docs/installation[Podman] or link:https://docs.docker.com/get-started/get-docker/[Docker]

* Valid credentials for link:registry.redhat.io[]

.Procedure

. In your CLI, authenticate to `registry.redhat.io`.

+
[source,bash]
----
podman login registry.redhat.io
----

. Pull the installer image.

+
[source,bash]
----
podman pull registry.redhat.io/rhtap-cli/rhtap-cli-rhel9:latest
----

. Start the `rhtap-cli` container image.

+
[source,bash]
----
$ podman run \
        -it \
        --entrypoint bash \ <1>
        --env-file tmp/private.env <2>
        --publish 8228:8228 \ <3>
        --rm \
        rhtap-cli:latest <4>
----

<1> Here bash is used so that we can have that shell
<2> Using an env file so that we do not have to disclose my credentials
<3> Publish to port to 8228 because we have a web service that’s going to interact with GitHub to create a GitHub application when we’re going to run the github app integration command in the later processes.
<4> The image tha you downloaed above.


= Creating config file

.Prerequisites

* `ClusterAdmin` access to an OpenShift cluster

.Procedure

. In the running container, login to your OpenShift cluster as ClusterAdmin.
+
[source,bash]
----
bash-5.1$ oc login https://api.<input omitted>.openshiftapps.com:443 --username cluster-admin --password <input omitted> 
----

. Create a `config.yaml` file:
+
[source,bash]
----
bash-5.1$ rhtap-cli config - - create 
----

This file creates a big chunk of configuration about how RHTAP is deployed.

. 


= Integrating products

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

== Integrating GitHub
{ProductShortName} uses GitHub to authenticate users. {ProductShortName} also uses GitHub as the destination for repositories that it generates.

To enable this functionality, before installing {ProductShortName} in your cluster, you must first complete the following procedures to configure GitHub for {ProductShortName}:

. Creating a GitHub personal access token

. Creating a GitHub application

. (Optional) Forking the software catalog

== Creating a GitHub personal access token

Before completing this procedure, you need to link:https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization#organization-owners[own a GitHub organization] that you can use for {ProductShortName}. This can be a new organization that you create, an organization you already own, or an existing organization for which you request ownership from the current admins. After installing {ProductShortName}, this GitHub organization gives {ProductShortName} users a place to create git repositories for their applications. 

Once you own an organization, you are ready to follow the steps in this procedure to create a personal access token. You need this token to run a command that is covered in the next procedure.

.Prerequisites:

* Ownership of a GitHub organization

.Procedure: 

. Go to your link:https://github.com/settings/apps[Developer Settings] page in GitHub. 

. In the left panel, under *Personal access tokens*, select *Tokens (classic)*.

. From the *Generate new token* drop down menu under the page banner, select *Generate new token (classic)*. You may need to authenticate to continue.

. Enter a name, select an expiration date, and under *Select scopes*, select *repo* (which should automatically include all scopes from *repo: status* to *security_events*). 

. Select *Generate token*. GitHub redirects you to a new page, where your token is visible. Create a new file called `private.env`, and save this token in that file.
+
NOTE: The `private.env` is critical to the success of your installation. Please ensure you create this file and save it in a secure location. 

== Creating a GitHub application for {ProductShortName}

Creating a GitHub application for {ProductShortName} allows developers to authenticate to Red Hat Developer Hub, which is the user interface (UI) where they can interact with RHTAP. This GitHub application also allows RHTAP to access developer’s source code that is hosted on GitHub.

Keep in mind that you must create and install the new application in the GitHub organization that you are using for {ProductName}. {ProductShortName} can subsequently create new repositories within that organization, to serve as the source code for the applications it builds.

Also be aware that this procedure directs you to pull and start running the installer container image. This installer allows you to automate much of the remaining installation process.  

.Prerequisites

* A GitHub personal access token (from the previous procedure)

* A container management tool on your workstation, such as link:https://podman.io/docs/installation[Podman] or link:https://docs.docker.com/get-started/get-docker/[Docker]

* Valid credentials for link:registry.redhat.io[]

* ClusterAdmin access to an OpenShift cluster

.Procedure

. Run the following command to start creating a GitHub application. Replace $GH_TOKEN with the token you created in the previous procedure. Replace $GH_ORG_NAME with the name of the GitHub organization you are using for {ProductShortName}. Replace $GH_APP_NAME with a name you would like to use for your application. 
+
[source]
----
bash-5.1$ rhtap-cli integration github-app --create --token="$GH_TOKEN" --org="$GH_ORG_NAME" $GH_APP_NAME
----  

. The output of this command includes a URL. Use your web browser on your workstation to navigate to this address. When prompted, click *Create your GitHub App*.

. The button redirects you to GitHub. If necessary, authenticate in GitHub to confirm access. Then click *Create GitHub App for <your organization's name>*.

. A new message displays in your browser, telling you that the app was successfully created. Click on the hyperlinked text to install the new application in your GitHub organization.

. The link redirects you to GitHub. Click the green *Install* button.

. Select the organization that you are using for {ProductShortName}.

. When prompted, select *All repositories*, so {ProductShortName} can create new repositories in your organization. Click the green *Install* button.
+
NOTE: You may want to keep this GitHub page open, although you can close it without interrupting installation. In the page banner, there is a link that you can use after installation to access {ProductShortName} (beginning with `\https://backstage-developer-hub-rhtap...`).

== (Optional) Forking the {ProductShortName} catalog repository

{ProductShortName} provides users with a set of software templates that enable developers to build applications more quickly. You may want to customize these templates, to tailor them to your users' specific needs. To enable this customization, you must fork the repository that contains the default templates now. In a later stage of the installation process, you can configure {ProductShortName} to find software templates in your customizable fork, rather than in the default repository.

.Procedure: 

. In your web browser, navigate to the link:https://github.com/redhat-appstudio/tssc-sample-templates[{ProductShortName} software catalog repository].

. Beneath the banner of the page, select *Fork* and fork the repository.
.. Uncheck the box that says "Copy the `main` branch only". 

. Once the fork is ready, copy its address. Label and save it in `private.env`.

. In your new fork, beneath the banner, click *main* to open a dropdown menu. Under *Tags*, select the release that corresponds to the version of {ProductShortName} that you are using.
+
NOTE: Be sure to update your fork from time to time, so updates from the upstream repository can benefit your instance of {ProductShortName}.

== (Optional) Integrating ACS 

.Prerequisites

* Administrator access to an instance of ACS

.Procedure

. Before you can integrate your instance of ACS, you need an API token and the central endpoint URL.
.. Follow the instructions for the prerequisites link:https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_security_for_kubernetes/{ACSVersion}/html/configuring/configure-api-token#create-api-token_configure-api-token[here] to create an API token. Save the token in `private.env`.
.. Follow the instructions link:https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_security_for_kubernetes/{ACSVersion}/html/configuring/configure-endpoints#configure-endpoints-existing_configure-endpoints[here] to configure your endpoint. Save the URL in `private.env`.

. In your `rhtap-cli` container, run the integration command. Replace $ACS_ENDPOINT with your ACS central endpoint URL, and $ACS_TOKEN with your ACS API token.
+
[source]
--
bash-5.1$ rhtap-cli integration acs --endpoint="$ACS_ENDPOINT" --token="$ACS_TOKEN"
--

== (Optional) Integrating Quay

In this procedure, you obtain two values from your instance of Quay. Then you integrate your instance into {ProductShortName}.

.Prerequisites:

* A link:http://Quay.io[Quay] account

* Ownership of a Quay link:https://docs.quay.io/glossary/organizations.html[organization] (you can use any plan, including the free option). 

NOTE: We recommend using a link:https://docs.redhat.com/en/documentation/red_hat_quay/{QuayVersion}/html/use_red_hat_quay/allow-robot-access-user-repo#allow-robot-access-user-repo[robot account] in Quay for this procedure. This way, once {ProductShortName} is installed, multiple users can authenticate to your organization's namespace in Quay.

.Procedure:

. In your web browser, login to Quay. On the right side of the banner, select your username and select *Account Settings* from the dropdown menu.

. On your user settings page, under *Docker CLI Password*, select *Generate Encrypted Password*. In the popup window, enter your password to authenticate.

. Next, still in the popup window, select *Docker Configuration > View [username]-auth.json*. Copy the string, without the quotation marks, following `"auth":`.

. In your `private.env` file, label and create the Docker configuration value with the following format, using your username and auth token where appropriate: {"auths": {"quay.io": {"auth": "[auth token]","email": ""}}}

. Back in the Quay UI, return to the link:https://quay.io/repository/[default Repositories page]. On the right side, under *Users and Organizations*, select the Quay organization you want to use for {ProductShortName}. 

. From the tabs on the left side, select *Applications*.

. Click *Create New Application*. Give your application a name.

. Click on the application's name. 

. From the tabs on the left, select *Generate Token*. 

. From the options for permissions for the token, select *View all visible repositories*.

. Click *Generate Access Token.*

. Click *Authorize Application*.

. The UI displays an access token. Label and save this token in `private.env`, too.

. In your `rhtap-cli` container, run the following command to integrate your instance of Quay. Replace $QUAY_DOCKERCONFIGJSON with the Docker configuration value. Replace $QUAY_TOKEN with the token you just generated. And replace $QUAY_URL with the address for your instance of Quay (https://quay.io if you have not installed Quay in your cluster).
+
[source]
--
bash-5.1$ rhtap-cli integration quay --dockerconfigjson='$QUAY_DOCKERCONFIGJSON' --token="$QUAY_TOKEN" --url="$QUAY_URL"
--

NOTE: Make sure to put the $QUAY_DOCKERCONFIGJSON value inside single quotes.

== (Optional) Integrating Bitbucket 

If you want to use Bitbucket cloud to host your source code, complete the steps in the following procedure.

.Prerequisites

* A Bitbucket username; to find your username:

.. On the sidebar in Bitbucket, click your profile picture and select *View profile*.

.. In the sidebar, select *Settings*. The system displays your username in the account settings.

* An link:https://support.atlassian.com/bitbucket-cloud/docs/app-passwords/[app password]

.Procedure

. In your `rhtap-cli` container, run the integration command. Replace $BB_USERNAME with your Bitbucket username, and $BB_TOKEN with your Bitbucket access tokens. If you are integrating with a custom Bitbucket host, replace $BB_URL with you Bitbucket host URL. If you are using the default `bitbucket.org` host, you can remove the `--host` option. 

+
[source,bash]
--
bash-5.1$ rhtap-cli integration bitbucket --username="$BB_USERNAME" --app-password="$BB_TOKEN" --host="$BB_URL"
--

== (Optional) Integrating Azure 
If you want to integrate Azure with {ProductName}, complete the steps in the following procedure.

.Prerequisites

* You must have the necessary permissions in your Azure subscription to register applications and manage API permissions.

* You must register a personal access token (PAT). For detailed steps, see https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops[How to generate personal access tokens in Azure DevOps].


* You must collect the following values:

** `AZURE_ORGANIZATION`: The name of your Azure DevOps organization. For example, `my-org-name`.

** `AZURE_HOST_URL`: The base URL of your Azure DevOps environment. The default is `dev.azure.com`.

* Optional values, required only if you authenticate using a registered Azure Active Directory (AAD) application:

** `AZURE_TENANT_ID`: The Directory (tenant) ID. See https://learn.microsoft.com/en-us/partner-center/find-ids-and-domain-names[Find your tenant ID].

** `AZURE_CLIENT_ID`: The Application (client) ID. See https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app[Register an application with the Microsoft identity platform].

** `AZURE_CLIENT_SECRET`: The client secret generated in the AAD app. See https://learn.microsoft.com/en-us/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps#create-a-client-secret[Create a client secret].

.Procedure

. In your `rhtap-cli` container, run the integration command after replacing the placeholder values with your Azure DevOps credentials. Additionally, if you are using the default host (`https://dev.azure.com`), you can omit the `--host` option.
+
[source,bash]
----
bash-5.1$ rhtap-cli integration azure \
  --organization="$AZURE_ORGANIZATION" \
  --host="$AZURE_HOST_URL" \
  --token="$AZURE_API_TOKEN" \
  // Append only if you are using Microsoft authentication
  --tenantID="$AZURE_TENANT_ID" \
  --client-id="$AZURE_CLIENT_ID" \
  --client-secret="$AZURE_CLIENT_SECRET"
----

== (Optional) GitHub Actions 

If you want to use GitHub Actions as an alternative CI provider, you do not need to complete any additional steps before installation. The GitHub application that you already made enables this CI functionality for {ProductShortName}.

== (Optional) Integrating GitLab 

If you want to use GitLab to host your source code, or as a CI provider, complete the steps in the following procedure.

== (Optional) Integrating GitLab

If you want to use GitLab to host your source code or as a CI provider, complete the steps in the following procedure.

.Prerequisites

* You must have the necessary permissions to create and manage GitLab jobs.
* You must have a personal access token. For instructions, see https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html[GitLab API token].
* You must have a GitLab host URL if you plan to integrate with a custom GitLab host. If you do not specify a GitLab host URL, the system defaults to `gitlab.com`.
* You must have the GitLab group name that contains your repositories.

.Procedure

. In your `rhtap-cli` container, run the integration command after replacing the placeholder values with your GitLab token, host URL, and group name. Additionally, if you are using the default GitLab host (`gitlab.com`), you can omit the `--host` option.

[source,bash]
----
bash-5.1$ rhtap-cli integration gitlab --token="$GL_API_TOKEN" --host="$GL_URL" --group="$GL_GROUP"
----

== (Optional) Integrating Jenkins 

.Prerequisites

* You must have the necessary permissions to create and manage Jenkins jobs.

*  You must have a URL using which you access Jenkins, a Jenkins user ID, and an link:https://www.jenkins.io/blog/2018/07/02/new-api-token-system/[API token].


.Procedure

. In your `rhtap-cli` container, run the integration command. Replace $JK_API_TOKEN with your Jenkins API token, $JK_URL with you Jenkins instance URL, $JK_USERNAME with your Jenkins user ID.

+
[source,bash]
--
bash-5.1$ rhtap-cli integration jenkins --token="$JK_API_TOKEN" --url="$JK_URL" --username="$JK_USERNAME"
--

== (Optional) Integrating JFrog Artifactory 

.Prerequisites

* Admin access to an instance of Artifactory

* A repository in Artifactory that you want to use with {ProductShortName}

.Procedure

. In the Artifactory UI, in the *Administration* view, click the green *Set Up Client/CI Tool* button next to the repository that you want to use.

. Select *Docker Client*

. Follow the UI instructions to authenticate in your CLI. 
.. The UI generates a token to use as a password. _Make sure to save it in `private.env`._
.. When you login to JFrog in your CLI, you should get a message saying your password has been stored in a location such as `~/.docker/config.json`. If you do not see this message, a later step in this procedure explains what to do.

. In your `rhtap-cli` container, run the integration command. Set the value of AF_URL to the URL of your instance (for example, "https://myusername.jfrog.io"). Set the value of AF_DOCKERCONFIGJSON to the contents of the file where your password was stored. Set the value of AF_API_TOKEN to the token that JFrog generated.
+
[source,bash]
--
bash-5.1$ rhtap-cli integration artifactory --url="$AF_URL" --dockerconfigjson='$AF_DOCKERCONFIGJSON' --token="$AF_API_TOKEN"
--

[NOTE]
====
Make sure to put the $AF_DOCKERCONFIGJSON value inside single quotes. Additionally, if your CLI did not print a message about the `config.json` file, you can create its contents as follows:
`{ "auths": { "<URL for your JFrog instance>":{ "auth": "<base64 format of username:password>", "email": "" }}}`
====

= Customizing config.yaml file 

You must customize the yaml file if you integrated _any_ of the above.

.Procedures

. Login to your Openshift cluster UI.
. In the Administrator view, select Workdloads > ConfigMaps
. Select RHTAP project, select rhtap-cli-config
. Select YAML view and navigate to where config.yaml parameters are defined.
. Complete the following:

.. If you forked the software catalog, update the `catalogURL` property to use the URL for your fork.

+
[source,yaml]
----
redhatDeveloperHub:
  enabled: &dhEnabled true
  namespace: &rhdhNamespace rhtap-dh
  properties:
    catalogURL: https://github.com/<your-username>/tssc-sample-templates/blob/releases/all.yaml
----

.. If you ran `rhtap-cli` integration commands, then change the values for the relevant `enabled` fields to `false`. The example below shows the change you need to make for integrating a pre-existing instance of ACS.

+
[source,yaml]
----
redhatAdvancedClusterSecurity:
  enabled: &acsEnabled false
  namespace: rhacs
----

+
[NOTE]
====
If you try to integrate outside products or pre-existing instances, but do not customize `config.yaml`, {ProductName} still installs and uses its default products. You must customize `config.yaml` for your `rhtap-cli integration` commands to take effect. However, if you do not customize `config.yaml` for your `rhtap-cli integration`, the installer deploys the product and overrides the existing integrations.
====

.. To use a custom namespace instead of the default one, configure the `namespacePrefixes` property in the `redhatDeveloperHub` section of the `config.yaml` file. By default, {ProductShortName} creates four namespaces during installation:

** `rhtap-app-ci`: For CI pipeline workloads
** `rhtap-app-development`, `rhtap-app-stage`, and `rhtap-app-prod`: For development, staging, and prod deployments

+
You can customize the prefixes for these namespaces and define additional namespace sets by using the `namespacePrefixes` property. For example, you can configure custom prefixes to generate namespaces such as `my_prefix1-app-ci`, `my_prefix1-app-development`, `my_prefix1-app-stage`, and `my_prefix1-app-prod`.

+
[source,yaml]
----
redhatDeveloperHub:
  namespacePrefixes:
    - my_prefix1
    - my_prefix2
----

. After you complete all necessary changes, select the save button.

== Installing {ProductShortName} with the `rhtap-cli deploy` command

If you have configured GitHub and, if necessary, customized `config.yaml`, then you are ready to install {ProductShortName}.

.Prerequisites 

* A running installer container, which is logged in to your OCP cluster as ClusterAdmin.

* None of the following operators are already installed in your cluster: 
** Advanced Cluster Security
** AMQ Streams
** Crunch-Data PostgreSQL
** Developer Hub
** Keycloak
** OpenShift GitOps 
** OpenShift Pipelines
** Quay
** Trusted Artifact Signer

.Procedure

. In the `rhatp-cli` container, run the installation command.
+
NOTE: Installation takes about fifteen minutes to complete.
+
[source]
--
bash-5.1$ rhtap-cli deploy
--

. Once installation is complete, be sure to save the output of the `rhtap-cli deploy` command in your `private.env` file. This output enables you to access your instances of the new products that are now installed. 

. Now, you can access your instance of {ProductShortName}! 
.. After creating a GitHub app, you may have left the page for your new GitHub app open, as our note suggested. In that case, you can use the link in the banner of that page to access {ProductShortName}. 
.. Otherwise, navigate to your the link:https://github.com/settings/apps[*Authorized GitHub Apps*] tab on your Applications page. Click on the name of the app you created for {ProductShortName}. Again, in the banner of this page, you can find the link you need to access {ProductShortName}, which begins with `\https://backstage-developer-hub-rhtap...`.
