:_mod-docs-content-type: PROCEDURE

[id="integrating-gitlab_{context}"]
= Integrating GitLab

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
