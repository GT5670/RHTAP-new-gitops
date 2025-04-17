:_mod-docs-content-type: PROCEDURE

[id="integrating-quay_{context}"]
= (Optional) Integrating Quay

Use this procedure to integrate an existing Quay organization or a self-hosted Quay instance with {ProductShortName} as your container image registry.

You will obtain two values from your Quay instance and then use them to complete the integration.

.Prerequisites

* A link:http://quay.io[Quay] account
* Ownership of a Quay link:https://docs.quay.io/glossary/organizations.html[organization]. Any plan, including the free option, is supported.

[NOTE]
====
Red Hat recommends using a robot account for this integration instead of a user account. A robot account allows automated systems and multiple users to authenticate to the Quay namespace after {ProductShortName} is installed.

To learn how to create and configure a robot account, see: link:https://docs.redhat.com/en/documentation/red_hat_quay/{QuayVersion}/html/use_red_hat_quay/allow-robot-access-user-repo#creating-robot-account-v2-ui[Create and use a robot account in Red Hat Quay]. 
====

.Procedure

. In a web browser, log in to Quay.

. On the right side of the page header, click your username, and then select *Account Settings* from the dropdown menu.

. On the *Account Settings* page, under *Docker CLI Password*, click *Generate Encrypted Password*. When prompted, enter your password to authenticate.

. In the same popup window, click *Docker Configuration > View [username]-auth.json*. Copy the string value (without quotation marks) that follows `"auth":`.

. In your `private.env` file, define the Docker configuration using your username and `auth` token in the following format:
+
[source,json]
----
{"auths": {"quay.io": {"auth": "[auth token]", "email": ""}}}
----

. In the Quay web UI, go to the link:https://quay.io/repository/[Repositories page].

. On the right side of the page, under *Users and Organizations*, click the organization you want to use with {ProductShortName}.

. In the left-hand navigation, click *Applications*.

. Click *Create New Application*, and enter a name for your application.

. Click the name of the application that you created.

. In the left-hand navigation, click *Generate Token*.

. In the permissions list, select *View all visible repositories*.

. Click *Generate Access Token*.

. Click *Authorize Application*. The UI displays the access token. Save this token in your `private.env` file.

. In your `rhtap-cli` container, run the following command to integrate Quay:
+
[source,bash]
----
bash-5.1$ rhtap-cli integration quay \
  --dockerconfigjson='$QUAY_DOCKERCONFIGJSON' \
  --token="$QUAY_TOKEN" \
  --url="$QUAY_URL"
----
Replace the following variables:
* `$QUAY_DOCKERCONFIGJSON`: The Docker configuration string you saved earlier
* `$QUAY_TOKEN`: The access token you generated in Quay
* `$QUAY_URL`: The URL of your Quay instance (for example, `https://quay.io`)
+
[NOTE]
====
Make sure to enclose the `$QUAY_DOCKERCONFIGJSON` value in single quotes to preserve JSON formatting.
====
