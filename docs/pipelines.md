:_mod-docs-content-type: PROCEDURE

[id="integrating-quay_{context}"]
= Integrating Quay

Integrate an existing Quay organization or self-hosted Quay instance with RHTAP to use it as your container image registry. In this procedure, you obtain two values from your instance of Quay. Then you integrate your instance into {ProductShortName}.

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
