== Enabling Argo CD Rollouts

The optional Argo CD Rollouts feature enhances Kubernetes by providing advanced deployment strategies, such as blue-green and canary deployments, for your applications. When integrated into the backstage Kubernetes plugin, it allows developers and operations teams to visualize and manage Argo CD Rollouts seamlessly within the Backstage interface.

.Prerequisites

* The Backstage Kubernetes plugin (`@backstage/plugin-kubernetes`) is installed and configured. 

** To install and configure Kubernetes plugin in Backstage, see link:https://backstage.io/docs/features/kubernetes/installation/[Installaltion] and link:https://backstage.io/docs/features/kubernetes/configuration/[Configuration] guide.

* You have access to the Kubernetes cluster with the necessary permissions to create and manage custom resources and `ClusterRoles`.

* The Kubernetes cluster has the `argoproj.io` group resources (for example, Rollouts and AnalysisRuns) installed.

.Procedures

. In the `app-config.yaml` file in your Backstage instance, add the following `customResources` component under the `kubernetes` configuration to enable Argo Rollouts and AnalysisRuns:

+
[source,yaml]
----
kubernetes:
  ...
  customResources:
    - group: 'argoproj.io'
      apiVersion: 'v1alpha1'
      plural: 'Rollouts'
    - group: 'argoproj.io'
      apiVersion: 'v1alpha1'
      plural: 'analysisruns'
----

. Grant `ClusterRole` permissions for custom resources.

.. If the Backstage Kubernetes plugin is already configured, the `ClusterRole` permissions for `Rollouts` and `AnalysisRuns` might already be granted.

+
[NOTE]
====
Use a link:https://raw.githubusercontent.com/backstage/community-plugins/main/workspaces/redhat-argocd/plugins/argocd/manifests/clusterrole.yaml[prepared manifest] for a read-only `ClusterRole` that provides access for both the Kubernetes plugin and the ArgoCD plugin.
====

.. If the `ClusterRole` permission is not granted, use the following YAML manifest to create the `ClusterRole`:

+
[source,yaml]
----
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: backstage-read-only
rules:
  - apiGroups:
      - argoproj.io
    resources:
      - Rollouts
      - analysisruns
    verbs:
      - get
      - list
----

.. Apply the manifest to the cluster using `kubectl`:
+
[source,bash]
----
kubectl apply -f <your-clusterrole-file>.yaml
----

.. Ensure the `ServiceAccount` accessing the cluster has this `ClusterRole` assigned.

. Add annotations to `catalog-info.yaml` to identify Kubernetes resources for Backstage.

.. For identifying resources by entity ID:
+
[source,yaml]
----
annotations:
  ...
  backstage.io/kubernetes-id: <BACKSTAGE_ENTITY_NAME>
----

.. (Optional) For identifying resources by namespace:
+
[source,yaml]
----
annotations:
  ...
  backstage.io/kubernetes-namespace: <RESOURCE_NAMESPACE>
----

.. For using custom label selectors (takes precedence over the above annotations):
+
[source,yaml]
----
annotations:
  ...
  backstage.io/kubernetes-label-selector: 'app=my-app,component=front-end'
----

. Add label to Kubernetes resources to enable Backstage to find the appropriate Kubernetes resources.

.. Backstage Kubernetes plugin label: Add this label to map resources to specific Backstage entities.
+
[source,yaml]
----
labels:
  ...
  backstage.io/kubernetes-id: <BACKSTAGE_ENTITY_NAME>
----

.. GitOps application mapping: Add this label to map Argo CD Rollouts to a specific GitOps application
+
[source,yaml]
----
labels:
  ...
  app.kubernetes.io/instance: <GITOPS_APPLICATION_NAME>
----

+
[NOTE]
====
If using the label selector annotation (backstage.io/kubernetes-label-selector), ensure the specified labels are present on the resources. The label selector will override other annotations like kubernetes-id or kubernetes-namespace.
====

.Verification

. Push code changes to your GitOps repository to trigger a deployment.

. Open the Backstage interface and navigate to the entity you configured.

. Confirm that the Argo CD Rollouts feature is functioning as expected by performing the following checks:

** Kubernetes resources, such as `Rollouts` and `AnalysisRuns`, are visible under the *Kubernetes* tab.

** You are able to monitor `Rollouts` status and manage deployments.

[role="_additional-resources"]
.Additional resources

* The package path, scope, and name of the {company-name} ArgoCD plugin has changed since 1.2. For more information, see link:{release-notes-url}#removed-functionality-rhidp-4293[Breaking Changes] in the _{rn-product-title}_. 

* For more information on installing dynamic plugins, see link:{installing-and-viewing-dynamic-plugins-url}[{installing-and-viewing-dynamic-plugins-title}].
