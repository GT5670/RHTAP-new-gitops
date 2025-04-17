:_mod-docs-content-type: PROCEDURE

[id="customizing-the-config-file_{context}"]
= Customizing the `config.yaml` file

Use this procedure to customize the `config.yaml` file before integrating products and external services. Customizing this file ensures that your integrations and preferences are respected during installation.

.Prerequisites

* You plan to integrate at least one product or external service (For example, {RHACSShortName} or Quay).

* (Optional) Forked software catalog repository URL. {ProductShortName} provides a catalog of software templates that help developers scaffold applications. To customize these templates, fork the repository before installation.

.. In your browser, go to the link:https://github.com/redhat-appstudio/tssc-sample-templates[{ProductShortName} software catalog repository].

.. Click *Fork* to fork the repository.

... Uncheck the box labeled *Copy the `main` branch only*.

.. When the fork is created, copy its URL and save it in the `private.env` file.

.. In the forked repository, click *main* to open the branch/tag dropdown.

.. Under *Tags*, select the release that matches your {ProductShortName} version.
+
[NOTE]
====
Update your fork periodically to include changes from the upstream repository.
====

* You have access to the OpenShift Web Console.

.Procedure

. In the OpenShift console, switch to the *Administrator* perspective.

. Go to *Workloads* > *ConfigMaps*.

. From the Project drop down list, select {ProductShortName}.

. Open the `rhtap-cli-config` ConfigMap.

. Select the *YAML* view and navigate to where `config.yaml` parameters are defined.

. Update the following fields as needed:

.. To use a custom software catalog, set the `catalogURL`:
+
[source,yaml]
----
redhatDeveloperHub:
  properties:
    catalogURL: https://github.com/<your-org>/tssc-sample-templates/blob/releases/all.yaml
----

.. To disable installation of components you've integrated externally (for example, ACS and Quay):
+
[source,yaml]
----
redhatAdvancedClusterSecurity:
  enabled: &rhacsEnabled false
  namespace: &rhacsNamespace rhtap-rhacs

redHatQuay:
  enabled: &quayEnabled false
  namespace: &quayNamespace rhtap-quay
----
+
[NOTE]
====
If you try to integrate outside products or pre-existing instances, but do not customize `config.yaml`, {ProductName} still installs and uses its default products. You must customize `config.yaml` for your `rhtap-cli integration` commands to take effect. However, if you do not customize `config.yaml` for your `rhtap-cli integration`, the installer deploys the product and overrides the existing integrations.
====

.. To use a custom namespace instead of the default one, configure the `namespacePrefixes` property in the `redhatDeveloperHub` section of the `config.yaml` file. By default, {ProductShortName} creates four namespaces during installation:

** `rhtap-app-ci`: For CI pipeline workloads
** `rhtap-app-development`, `rhtap-app-stage`, and `rhtap-app-prod`: For development, staging, and prod deployments
+
You can customize the prefixes for these namespaces and define additional namespace sets by using the `namespacePrefixes` property. For example, you can configure custom prefixes to generate namespaces such as `my_prefix1-app-ci`, `my_prefix1-app-development`, `my_prefix1-app-stage`, and `my_prefix1-app-prod`.
+
[source,yaml]
----
redhatDeveloperHub:
  namespacePrefixes:
    - my_prefix1
    - my_prefix2
----

. After you complete all necessary changes, select *Save*.
