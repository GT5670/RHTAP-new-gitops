:_newdoc-version: 2.18.3
:_template-generated: 2025-04-14
:_mod-docs-content-type: PROCEDURE

[id="integrating-jenkins_{context}"]
= Integrating Jenkins

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
