About Red Hat Developer Hub
Red Hat Developer Hub (RHDH) is an enterprise-grade internal developer portal designed to simplify and enhance software development processes. When combined with Red Hat OpenShift, it enables platform engineering teams to create customized developer portals that maximize developer productivity, ease onboarding, and accelerate application delivery. RHDH reduces friction and frustration for developers, allowing them to focus on writing high-quality code while aligning with organizational best practices.

RHDH provides a centralized platform that integrates software templates, pre-architected solutions, and dynamic plugins, offering tailored solutions for operations and development teams within a unified framework.

Benefits of Red Hat Developer Hub
For Developers:

Simplified access to tools, resources, and workflows through a centralized dashboard.
Self-service capabilities with guardrails for cloud-native development.
Streamlined software and service creation using pre-configured templates.

For System Architects:

Tailored platforms with curated tools to support developers efficiently.
Centralized repositories for consistent configuration management.
Simplified governance of technology choices and operational processes.

For Organizations:

Scalability to onboard new teams quickly while maintaining consistency.
Enhanced security with enterprise-grade Role-Based Access Control (RBAC).
Cost and time efficiency by mitigating cognitive load and eliminating workflow bottlenecks.

Key Features
Centralized Dashboard: Provides a single interface for accessing developer tools, CI/CD pipelines, APIs, monitoring tools, and documentation. Integrated with systems like Git, OpenShift, Kubernetes, and JIRA.

Dynamic Plugins: Add, update, or remove plugins dynamically without downtime. Popular plugins like Tekton, GitOps, Nexus Repository, and JFrog Artifactory are supported and verified by Red Hat.

Software Templates: Simplify development processes by automating tasks such as repository setup, variable insertion, and production pipeline creation.

Role-Based Access Control (RBAC): Manage user access with robust security permissions tailored to organizational needs.

Scalability: Support growing teams and applications while maintaining access to the same tools and services.

Configuration Management: Centralized repositories ensure synchronized updates, improving version control and environment configuration.

Integrations in RHDH
Integration with Red Hat OpenShift
RHDH is fully integrated with Red Hat OpenShift, offering features such as:

Operators to manage application lifecycles.
Seamless access to OpenShift capabilities, including service mesh, serverless functions, GitOps, and distributed tracing.
Supported pipelines and GitOps plugins for advanced workflows.


Integration with Red Hat trusted application pipeline
Installing Red Hat Trusted Application Pipeline (RHTAP) enhances Red Hat Developer Hub (RHDH) by adding secure CI/CD capabilities that integrate security measures into your development process from the start. While RHDH focuses on the inner loop (code, build, and test), RHTAP covers the outer loop by automating code scanning, image building, vulnerability scanning, and deployment. 

RHTAP includes tools like Red Hat Trusted Artifact Signer (RHTAS) for code integrity, Red Hat Trusted Profile Analyzer (RHTPA) for automated Software build of Materials (SBOM) creation, and Red Hat Advanced Cluster Security (RHACS) for vulnerability scanning. 

Together RHTAP and RHDH provide an end-to-end solution that simplifies and secures your software development lifecycle.

Extending Backstage with RHDH
RHDH extends the upstream Backstage project by adding:

Enhanced search capabilities that aggregate data from CI/CD pipelines, cloud providers, source control, and more.
A centralized software catalog for locating applications, APIs, and resources.
Automation through open-source plugins that expand Backstage’s core functionality.
Simplified tech documentation using Markdown and Git, with integrated search for easy navigation.


[role="_additional-resources"]
== Next steps
* link:https://docs.redhat.com/en/documentation/red_hat_developer_hub/{product-version}#Install%20and%20Upgrade[{product} Installation and upgrade guides]

[role="_additional-resources"]
== Additional resources

* link:https://docs.redhat.com/en/documentation/red_hat_trusted_application_pipeline/{rhtap-version}/html/getting_started_with_red_hat_trusted_application_pipeline/index[Getting Started with Red Hat trusted application pipeline]
* link:https://docs.redhat.com/en/documentation/openshift_container_platform[OpenShift documentation]
