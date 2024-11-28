:_mod-docs-content-type: CONCEPT
[id="con_about-rhtap_{context}"]

= About {ProductName}

Securing your software supply chain is critical to prevent software vulnerabilities. {ProductName} embeds security throughout the software development lifecycle (SDLC), enabling teams to innovate confidently while adhering to the highest security standards.

== Overview

{ProductShortName} is a DevSecOps framework that integrates security from project inception to production. It incorporates advanced security practices to ensures that your software is resilient to threats while streamlining development processes.

=== Key features

* *Secure CI/CD pipelines*: Build, test, and deploy container images securely using pre-configured pipelines integrated with your Git repository.

* *Ready-to-use templates*: Start project quickly with customizable templates that apply secure development practices.

* *Vulnerability management*: Detect and address potential vulnerabilities with detailed insights, including automated generation of Software Bills of Materials (SBOMs).

* *Compliance with Enterprise Contracts*: Maintain regulatory compliance at every stage of the development process with our robust enforcement of security and quality standards.

=== Integrated technologies

{ProductShortName} integrates with industry-leading platforms and tools:

[cols="1,1"]
|===
|Component or Technology |Description

| {RHDHLongName} ({RHDHShortName}) | A self-service portal that streamlines development and integrates security best practices from the get-go.

| {RHTASLongName} ({RHTASShortName}) | Enhances software integrity through signature and attestation, ensuring all artifacts are secure and authentic.

| {RHTPALongName} ({RHTPAShortName}) | Automates the creation and management of SBOMs, providing transparency and compliance in your software supply chain.

| {RHACSLongName} ({RHACSShortName}) | Automates the scanning of artifacts for vulnerabilities.

| OpenShift GitOps | Manages Kubernetes deployments and infrastructure using Git repositories, ensuring consistent, automated, and secure deployment practices.

| OpenShift Pipelines | Automates the CI/CD processes with visibility and control over build, test, and deployment workflows.

| Argo CD | Automates application deployment and lifecycle management, ensuring consistent versions of app definitions, configurations, and environments.

|===

=== Flexible configuration options

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

== How it works

{ProductShortName} integrates security at every step of the DevSecOps workflow:

* *Start with secure templates:* Leverage pre-built templates from {RHDHLongName} ({RHDHShortName}) for a secure foundation. These templates include code repositories, documentation, and pre-configured CI/CD pipelines.

* *Develop and modify code:* Modify your code after creating the application. Each code change triggers a pipeline run that automatically performs security checks, including artifact signing, vulnerability scanning, and SBOM generation.

* *Managed deployment:* {ProductShortName} enforces security policies throughout the development lifecycle, from development to production, using Enterprise Contracts (EC). This ensures that only compliant builds are deployed.

[role="_additional-resources"]
.Next step

* For more information about getting started with {ProductShortName}, see link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html-single/getting_started_with_red_hat_trusted_application_pipeline[Getting Started with {ProductName}].

[role="_additional-resources"]
.Additional Resources

* For more information about {RHDHLongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_developer_hub[Red Hat Developer Hub Documentation].

* For more information about {RHTASLongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_trusted_artifact_signer/1/html-single/deployment_guide[Red Hat Trusted Artifact Signer Deployment Guide].

* For more information about {RHTPALongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_trusted_profile_analyzer[Red Hat Trusted Profile Analyzer Documentation].
