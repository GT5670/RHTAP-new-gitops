:_newdoc-version: 2.18.3
:_template-generated: 2025-04-14
:_mod-docs-content-type: PROCEDURE

[id="integrating-jfrog-artifactory_{context}"]
= Integrating JFrog Artifactory

Write a short introductory paragraph that provides an overview of the module. The introduction should include what the module will help the user do and why it will be beneficial to the user. Include key words that relate to the module to maximize search engine optimization.

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

+
NOTE: Make sure to put the $AF_DOCKERCONFIGJSON value inside single quotes. Additionally, if your CLI did not print a message about the `config.json` file, you can create its contents as follows:
`{ "auths": { "<URL for your JFrog instance>":{ "auth": "<base64 format of username:password>", "email": "" }}}`

