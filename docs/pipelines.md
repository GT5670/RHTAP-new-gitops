:_mod-docs-content-type: CONCEPT
[id="con_about-rhtap_{context}"]

= About {ProductName}

In an era where software vulnerabilities can have far-reaching consequences, securing your software supply chain is critical. {ProductName} ({ProductShortName}) is designed to embed security throughout the software development lifecycle (SDLC), enabling teams to innovate confidently while adhering to the highest security standards.

== What is {ProductShortName}?

{ProductShortName} is more than a CI/CD platform—it’s a comprehensive DevSecOps framework that integrates security from project inception to production. By incorporating advanced security practices, {ProductShortName} ensures your software is resilient to emerging threats, while also streamlining development processes.


=== Features that define {ProductShortName}

* *Secure CI/CD Pipelines*: Build, test, and deploy container images securely using pre-configured pipelines integrated with your Git repository.

* *Ready-to-Use Templates*: Accelerate project initiation with customizable templates, ensuring secure development practices are applied from the start.

* *Advanced Vulnerability Scanning*: Detect and address potential vulnerabilities with detailed insights, including automated generation of Software Bills of Materials (SBOMs).

* *Enterprise Contract Enforcement*: Maintain compliance by enforcing stringent quality and security rules at every stage of development.

== Who should use {ProductShortName}?

Designed for platform engineers, application developers, and security teams, {ProductShortName} is ideal for organizations looking to enhance the security and efficiency of their software supply chains. Whether you are establishing a new CI/CD process or optimizing an existing one, {ProductShortName} provides the tools and flexibility you need.

== How Does {ProductShortName} work?

{ProductShortName} empowers organizations to secure and streamline their DevSecOps CI/CD workflows with a comprehensive suite of tools:

=== Secure development from the day one

Access pre-built templates in {RHDHLongName}, which include code repositories, documentation, and CI/CD pipelines to streamline the onboarding process.

=== Continuous security and compliance

Each code modification triggers security checks, including artifact signing, vulnerability scanning, and SBOM generation, ensuring compliance with enterprise standards.

=== Managed deployment

From development to production, {ProductShortName} enforces security policies through Enterprise Contracts, ensuring only compliant builds are deployed.

== Technologies underpinning {ProductShortName}

{ProductShortName} integrates seamlessly with industry-leading platforms and tools to maintain security and efficiency:

[cols="1,1"]
|===
|Component or Technology |Description

| {RHDHLongName} ({RHDHShortName}) | The self-service portal streamlines development and integrates security best practices from the start.

| {RHTASLongName} ({RHTASShortName}) | Enhances software integrity through signature and attestation, ensuring all artifacts are secure and authentic.

| {RHTPALongName} ({RHTPAShortName}) | Automates the creation and management of SBOMs, providing transparency and compliance in your software supply chain.

| {RHACSLongName} ({RHACSShortName}) | Automates the scanning your artifacts for vulnerabilities.

| OpenShift GitOps | Manages Kubernetes deployments and infrastructure using Git repositories, ensuring consistent, automated, and secure deployment practices.

| OpenShift Pipelines | Automates the CI/CD processes with visibility and control over build, test, and deployment workflows, accelerating your path to production while maintaining high-quality standards.

| Argo CD | Automates and tracks application deployment and lifecycle management, ensuring consistent versions of app definitions, configurations, and environments.

|===

== Flexibility in {ProductShortName}

{ProductShortName} provides flexibility in CI/CD management, source repositories, and registry for artifacts, allowing you to choose the tools that best fit your development needs:

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
* Jfrog Artifactory
|===

== Key Security Practices

{ProductShortName} incorporates advanced security measures to protect your software supply chain:

* *Vulnerability Scanning:* Each pull request undergoes thorough scans to detect and address potential security threats early in the development process.
* *SBOM Generation:* Automated SBOM generation provides a comprehensive inventory of software components, ensuring transparency and compliance.
* *Container Image Security:* Verifies container images comply with link:https://slsa.dev/[SLSA (Supply-chain Levels for Software Artifacts)] guidelines, enforced by an Enterprise Contract with comprehensive security rules.

== Why choose {ProductShortName}?
With its integrated security features, {ProductShortName} empowers team to adopt a proactive approach to securing software supply chain. From automated compliance checks to advanced vulnerability detection, it simplifies the complexities of DevSecOps, allowing organizations to focus on delivering high-quality software.

[role="_additional-resources"]
.Additional Resources

* For more information about getting started with {ProductShortName}, see link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{ProductVersion}/html-single/getting_started_with_red_hat_trusted_application_pipeline[Getting Started with {ProductName}].

* For more information about {RHDHLongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_developer_hub[Red Hat Developer Hub Documentation].

* For more information about {RHTASLongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_trusted_artifact_signer/1/html-single/deployment_guide[Red Hat Trusted Artifact Signer Deployment Guide].

* For more information about {RHTPALongName}, see link:https://access.redhat.com/documentation/en-us/red_hat_trusted_profile_analyzer[Red Hat Trusted Profile Analyzer Documentation].
