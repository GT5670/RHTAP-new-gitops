:_mod-docs-content-type: PROCEDURE

[id="deploy-application-and-view-security-insights_{context}"]
= Deploy application and view security insights

Organizations leverage a structured approach for application deployment, typically involving development, pre-production, and production stages. This process is often automated and governed by defined rules and triggers.

This guide outlines deploying applications through ArgoCD in OpenShift GitOps, enabling continuous deployment across all stages. ArgoCD facilitates a GitOps-based deployment strategy, treading your Git repository as a single source of truth for your infrastructure configurations. Updates to this repository trigger deployments across environments.

[NOTE]
====
This guide shows an example deployment approach; organizations may adopt any method that suits their workflow.
====

== Promoting a build to a pre-production or production environment

Promoting a build from one environment to another (like from development to stage or production) involves updating the GitOps repository through a pull request (PR).

. On {RHDHShortName} platform, select *Catalog*.

. From the *Kind* dropdown list, select *Resource*, and then select an appropriate GitOps repository.

. On the Overview tab, select *View Source*.

. (Optional) Alternatively, select *Catalog*, and then on the *Overview* tab, select *View TechDocs*

.. In the *Home* > *Repository* section, select the GitOps repository.

. Clone your GitOps repository, and go to the `component/<app-name>` directory.

+
[NOTE]
====
Ensure that the local clone is up-to-date.
====

. Checkout a new branch.

. Within the repository, locate the `component/<app-name>/overlays` directory, where you'll find the `development`, `stage`, and `prod` subdirectories, each correspond to an environment.

. Manually move an application from development environment to the stage or production environment.

+
[cols="1,1"]
|===
|To move your application|Do this

a|From development to stage environment
a|1. Expand `development` directory and select `deployment-patch.yaml`. 
2. Copy the containers image URL. For example, quay.io/<username>/<app-name>/imageurl. 
3. Go to `stage` directory, select `deployment-patch.yaml`, and replace the existing container image URL with the one copied.

NOTE: If you want to promote other configuration changes (for example, replicas) in addition to the container image from the development to the stage environment, copy the changes from the `deployment-patch.yaml` file located in the `development` directory and paste them into the `deployment-patch.yaml` file in the `stage` directory.


a|From stage to production environment
a|1. Expand `stage` directory and select `deployment-patch.yaml`. 
2. Copy the containers image URL. For example, quay.io/<username>/<app-name>/imageurl. 
3. Go to `prod` directory, select `deployment-patch.yaml`, and replace the existing container image URL with the one copied.

NOTE: If you want to promote other configuration changes (for example, replicas) in addition to the container image from the stage to the production environment, copy the changes from the `deployment-patch.yaml` file located in the `stage` directory and paste them into the `deployment-patch.yaml` file in the `prod` directory.
|===

. Commit and push your updates.

. Create a pull request (PR). This action initiates a promotion pipeline run that validates the updated container images against {ECLong} ({ECShort}) policies. The pipeline run visually represents all tasks, with a *green* status signifying successful completion. 

.. Review the promotion pipeline in the *CI* tab within {RHDHShortName}.

. Review and merge the PR. Merging the PR triggers ArgoCD, which then automatically applies the necessary changes to promote the build to the next environment. 

.. Review the latest deployment updates in the *CD* tab within {RHDHShortName}. It displays updates on the application's current status, deployment details, the author of the pipeline run, the commit message (for example, Promote stage to prod), and the container image advanced to production.

.Verification

* To assess the successful promotion of your application, navigate to the *Topology* tab. Here, you can review the application's distribution across the designated namespaces.
