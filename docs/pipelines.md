:_newdoc-version: 2.18.3
:_template-generated: 2025-04-14
:_mod-docs-content-type: PROCEDURE

[id="integrating-bitbucket_{context}"]
= Integrating Bitbucket

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
