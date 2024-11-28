:_mod-docs-content-type: CONCEPT
[id="con_about-rhtap_{context}"]

= About {ProductName}

Securing your software supply chain is critical to prevent software vulnerabilities. {ProductName} {ProductShortName} embeds security throughout the software development lifecycle (SDLC), enabling teams to innovate confidently while adhering to the highest security standards.

== Overview of {ProductShortName}

{ProductShortName} is a DevSecOps framework that integrates security from project inception to production. It incorporates advanced security practices to ensures that your software is resilient to threats while streamlining development processes.

=== Features of {ProductShortName}

* *Secure CI/CD pipelines*: Build, test, and deploy container images securely using pre-configured pipelines integrated with your Git repository.

* *Ready-to-use templates*: Start project quickly with customizable templates that apply secure development practices.

* *Advanced vulnerability scanning*: Detect and address potential vulnerabilities with detailed insights, including automated generation of Software Bills of Materials (SBOMs).

* *Enterprise contract enforcement*: Enforce quality and security rules at every stage of development to maintain compliance.

=== Technologies in {ProductShortName}

{ProductShortName} integrates with industry-leading platforms and tools:

[cols="1,1"]
|===
|Component or Technology |Description

| {RHDHLongName} ({RHDHShortName}) | A self-service portal that streamlines development and integrates security best practices from the start.

| {RHTASLongName} ({RHTASShortName}) | Enhances software integrity through signature and attestation, ensuring all artifacts are secure and authentic.

| {RHTPALongName} ({RHTPAShortName}) | Automates the creation and management of SBOMs, providing transparency and compliance in your software supply chain.

| {RHACSLongName} ({RHACSShortName}) | Automates the scanning of artifacts for vulnerabilities.

| OpenShift GitOps | Manages Kubernetes deployments and infrastructure using Git repositories, ensuring consistent, automated, and secure deployment practices.

| OpenShift Pipelines | Automates the CI/CD processes with visibility and control over build, test, and deployment workflows.

| Argo CD | Automates application deployment and lifecycle management, ensuring consistent versions of app definitions, configurations, and environments.

|===

=== Flexibility in {ProductShortName}

{ProductShortName} allows flexibility in CI/CD management, source repositories, and artifact registries:

[cols="1,1"]

|===
|Category |Options

|CI/CD pipelines
a|* Tekton (Default)
* Jenkins
* GitHub Actions
* Gitlab CI

NOTE: All CI pipelines expect Tekton conform to link:https://slsa.dev/spec/v1.0/levels[SLSA] Build L2. Tekton conforms to Build L3.

|Source repositories
a|* GitHub (Default)
* GitLab
* Bitbucket

|Artifact registries
a|* Quay (Default)
* JFrog Artifactory
|===

=== Target users of {ProductShortName}

{ProductShortName} is designed for platform engineers, application developers, and security teams who aim to enhance the security and efficiency of their software supply chains. It is suitable for organizations establishing a new CI/CD process or optimizing an existing one.

== How {ProductShortName} works

{ProductShortName} secures and streamlines DevSecOps CI/CD workflows by integrating security throughout the development process:

* *Start with secure templates:* Select pre-built templates in {RHDHLongName} {RHDHShortName} to create your application. These templates include code repositories, documentation, and CI/CD pipelines.

* *Develop and modify code:* After creating the application, modify the code. Each code change triggers a pipeline run that performs security checks, including artifact signing, vulnerability scanning, and Software Bill of Materials (SBOM) generation.

* *Managed deployment:* From development to production, {ProductShortName} enforces security policies through Enterprise Contracts (EC), ensuring only compliant builds are deployed.

[role="_additional-resources"]
.Next step

* For more information about getting started with {ProductShortName}, see link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html-single/getting_started_with_red_hat_trusted_application_pipeline[Getting Started with {ProductName}].

[role="_additional-resources"]
.Additional Resources

* For more information about {RHDHLongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_developer_hub[Red Hat Developer Hub Documentation].

* For more information about {RHTASLongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_trusted_artifact_signer/1/html-single/deployment_guide[Red Hat Trusted Artifact Signer Deployment Guide].

* For more information about {RHTPALongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_trusted_profile_analyzer[Red Hat Trusted Profile Analyzer Documentation].
