:_mod-docs-content-type: PROCEDURE

[id="integrating-github_{context}"]
= Integrating GitHub

{ProductShortName} uses GitHub to authenticate users and to create and manage application repositories. Before you install {ProductShortName}, you must configure GitHub to support these capabilities.

To enable GitHub integration, complete the following procedures:

. Create a GitHub personal access token.
. Create a GitHub application.

[discrete]
== Create a GitHub personal access token

You must own a GitHub organization before you create a personal access token.

You can use an existing GitHub organization, create a new one, or request ownership of an existing organization from its current administrators.

After installation, this GitHub organization provides a location where users can generate repositories for their applications.

You must create a personal access token (PAT) to complete the next procedure.

.Prerequisites

* Ownership of a GitHub organization

.Procedure

. Go to your link:https://github.com/settings/apps[Developer settings] page on GitHub.

. In the left navigation panel, under *Personal access tokens*, click *Tokens (classic)*.

. From the *Generate new token* dropdown menu, select *Generate new token (classic)*. Authenticate if prompted.

. Enter a name, select an expiration date, and under *Select scopes*, select *repo*. This automatically includes all scopes from `repo:status` to `security_events`.

. Click *Generate token*. GitHub redirects you to a new page where your token is displayed.

. (Optional) To use the token in future steps, save it in a file (for example, values.txt).


[discrete]
== Create a GitHub application

Creating a GitHub application for {ProductShortName} allows developers to authenticate to Red Hat Developer Hub, the web-based interface for interacting with {ProductShortName}. It also allows {ProductShortName} to access your GitHub organization and create repositories.

You must create and install this application in the same GitHub organization that you plan to use with {ProductShortName}. The installer automates much of the remaining setup.

.Prerequisites

* A GitHub personal access token

* Valid credentials for link:registry.redhat.io[]

* `cluster-admin` access to an OpenShift cluster

.Procedure

. Run the following command to create a GitHub application:
+
[source,bash]
----
bash-5.1$ rhtap-cli integration github-app \
  --create \
  --token="$GH_TOKEN" \
  --org="$GH_ORG_NAME" \
  $GH_APP_NAME
----
Replace the following variables:

* `$GH_TOKEN`: The GitHub personal access token
* `$GH_ORG_NAME`: The GitHub organization name
* `$GH_APP_NAME`: The name for your GitHub application

. Copy the URL from the command output and open it in a browser.

. When prompted, click *Create your GitHub App*.

. If required, authenticate to GitHub.

. Click *Create GitHub App for <your organization>*.

. When the app is created, a success message appears. Click the link in that message to install the application in your GitHub organization.

. On the redirected GitHub page, click the green *Install* button.

. Select the GitHub organization that you are using for {ProductShortName}.

. When prompted, select *All repositories*, and click *Install*.
+
[NOTE]
====
You may want to keep this GitHub page open. In the page banner, there is a link that you can use after installation to access {ProductShortName} (beginning with `\https://backstage-developer-hub-rhtap...`).
====

