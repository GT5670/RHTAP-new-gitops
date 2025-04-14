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

. In your CLI, authenticate to `registry.redhat.io`.
+
 $ podman login registry.redhat.io

. Pull the installer image.
+
 $ podman pull registry.redhat.io/rhtap-cli/rhtap-cli-rhel9:latest

. Start the `rhtap-cli` container image.
+
[source]
----
$ podman run \
        -it \
        --entrypoint=bash \
        --publish 8228:8228 \
        --rm \
        rhtap-cli:latest
----
. In the running container, login to your OpenShift cluster as ClusterAdmin.
+
[source]
----
bash-5.1$ oc login https://api.<input omitted>.openshiftapps.com:443 --username cluster-admin --password <input omitted> 
----

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
