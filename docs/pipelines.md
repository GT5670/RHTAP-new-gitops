:_mod-docs-content-type: PROCEDURE

[id="integrating-quay_{context}"]
= (Optional) Integrating Quay

Use this procedure to integrate an existing Quay organization or a self-hosted Quay instance with {ProductShortName} as your container image registry.

You must obtain two values from your Quay instance and use them when running the CLI command: a Docker configuration string and an access token.

.Prerequisites

* A link:http://quay.io[Quay] account
* Ownership of a Quay link:https://docs.quay.io/glossary/organizations.html[organization] (any plan is supported, including free)

[NOTE]
====
Red Hat recommends using a robot account for this integration instead of a user account. A robot account allows automated systems and multiple users to authenticate to the Quay namespace after {ProductShortName} is installed.

To learn how to create and configure a robot account, see:
link:https://docs.redhat.com/en/documentation/red_hat_quay/{QuayVersion}/html/use_red_hat_quay/allow-robot-access-user-repo#creating-robot-account-v2-ui[Create and use a robot account in Red Hat Quay].
====

.Procedure

. In a web browser, log in to your Quay account.

. On the top right of the page, click your username, and then select *Account Settings*.

. On the *Account Settings* page, under *Docker CLI Password*, click *Generate Encrypted Password*. When prompted, enter your password to authenticate.

. In the same popup, click *Docker Configuration* > *View [username]-auth.json*.  
  Copy the string value (without quotation marks) that follows `"auth":`.

. Save the `auth` value and your Quay username to a file, such as `values.txt`, for reuse in later steps to be used in the Docker configuration.

. In a separate browser tab, go to the link:https://quay.io/repository/[Repositories page].

. Under *Users and Organizations*, click the name of the organization you want to use with {ProductShortName}.

. In the left-hand navigation, click *Applications*.

. Click *Create New Application* and enter a name.

. Click the name of the application that you created.

. In the left-hand navigation, click *Generate Token*.

. In the permissions list, select *View all visible repositories*.

. Click *Generate Access Token*.

. Click *Authorize Application*. Quay displays the access token. Copy this token.

[NOTE]
====
You can use an OAuth application instead of a user or robot account. For more information, see:
link:https://access.redhat.com/documentation/en-us/red_hat_quay/3/html/manage_red_hat_quay/configure-oauth-applications[Create an OAuth application].

Only the *View all visible repositories* permission is required.
====

. In your `rhtap-cli` container, run the following command to integrate Quay with {ProductShortName}, passing all required values inline:
+
[source,bash]
----
bash-5.1$ rhtap-cli integration quay \
  --dockerconfigjson='{"auths":{"quay.io":{"auth":"<auth_token>","email":""}}}' \
  --token="<quay_access_token>" \
  --url="https://quay.io"
----
Replace the following values:
* `<auth_token>`: The value from the `auth.json` file under `"auth":`
* `<quay_access_token>`: The access token you generated via the OAuth application
* `https://quay.io`: The Quay instance URL (use your custom URL if self-hosted)

[NOTE]
====
Make sure to enclose the entire `--dockerconfigjson` value in single quotes to preserve JSON formatting.
====
