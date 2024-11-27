:_mod-docs-content-type: CONCEPT

[id="rhtap-workflow_{context}"]

= {ProductShortName} Workflow

The {ProductShortName} workflow involves key steps to create, update, secure, and deploy applications. It also allows integration with various repositories, container registries, and CI/CD tools for flexibility.

[cols="1,1", options="header"]
|===
| Step | Description

| Install {ProductShortName}
| Begin by installing {ProductShortName} in your environment to enable secure and efficient DevSecOps workflows.

| Create an Application
a| Use pre-built templates to create an application. These templates are customizable and include pipelines and configurations to simplify the development process. When creating an application you can choose:

* GitHub (default), Gitlab, or Bitbucket for repositories
* Quay (default) or Jfrog Artifactory for registries
* Tekton (default), GitHub Actions, Jenkins, or GitLab CI for CI/CD workflows

NOTE: If you select Bitbucket, GitLab, or Jenkins during application setup, you must configure these tools accordingly to integrate them with your pipeline.

| Update an Application
| Push updates to your application code as needed. The pipeline automatically processes and secures the changes.

| View Security Insights
| Pipeline runs provide a visual representation of all tasks, offering insights into security checks and compliance.

| Deploy an Application
| Progress your application from Development to Staging and eventually to Production environments.

| (Optional) Customize Templates and Pipelines 
| Modify templates and pipelines to align with your organization's specific requirements and development practices.

|===

[role="_additional-resources"]
.Next step

* xref:installing-red-hat-trusted-application-pipeline_{context}[Your path to secure application development]
