:_mod-docs-content-type: PROCEDURE

[id="update-code-and-view-security-insights_{context}"]
= Update code and view security insights

[role="_abstract"]
After successfully building your component with {ProductShortName}, the next step is to make a code change and delve into the security insights.

== Initiating code updates

With {ProductShortName}, this process is straightforward.

. Select *Catalog* and then select an appropriate component for which you want to view security insights.

. On the *Overview* tab, select *View Source* tab to see your project in GitLab or GitHub. Here, you can also select *View Tech Docs* to see your project's documentation. The source of the documentation is the `docs` directory in your repository. If you update these files and the pipeline runs successfully, your Tech Docs will update too.

== Making changes to your code

With access to your repository, you're ready to engage in the familiar process of working with a git repository. Here's how to proceed:

- **Clone** your repository to start working on it either locally or in your development environment.

- **Modify** your application, like updating technical docs or `index.html`, or by adding new features or bug fixes.

- *Commit* your changes.

- **Push** your changes to the repository.

[NOTE]
====
* You can also use *GitLab or GitHub* UI, to directly update your code within the web interface.

* *For GitLab users only:* You have to set up webhooks and secrets in GitLab to automatically trigger pipeline run upon code updates. For information on setting up webhooks and secrets in GitLab, refer to link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html-single/installing_red_hat_trusted_application_pipeline/index#optional_configuring_gitlab_webhooks_for_automated_pipeline_triggers[Configuring GitLab Webhooks for automated pipeline triggers].
====

== Viewing the pipeline run

To view the pipeline run after making changes to your code:

. Return to {RHDHShortName} platform to see how your changes progressed.
. Navigate to the *Catalog* and select the specific component you just modified.
. Open the *CI* tab to access the pipeline run.

Beyond the pipeline run, {RHDHShortName} offers valuable insights through other tabs:

* *CD*: Gain insights into deployments managed by ArgoCD and GitOps using the *CD* tab.

* *Topology*: Visualize your application's deployment within the development namespace with the *Topology* tab.
