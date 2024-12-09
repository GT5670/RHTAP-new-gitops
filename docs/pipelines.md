What is Red Hat Trusted Application Pipeline?
Red Hat® Trusted Application Pipeline helps software development teams enhance security with automatic, integrated checks that catch vulnerabilities early in the software supply chain. Organizations can then curate their own trusted, repeatable pipelines that stay compliant to industry requirements.

Built on proven, trusted open source technologies, Red Hat Trusted Application Pipeline is part of Red Hat Trusted Software Supply Chain, a set of solutions to protect users, customers, and partners from risks and vulnerabilities in their software factory.


Red Hat Trusted Application Pipeline overview. Video duration: 2:25

Features and benefits
Security-first development workspaces
Boost developer productivity with internal development platforms. Provide self-serve, validated software templates for building and deploying applications that follow defined security practices.

Integrated security checks
Scan and isolate security issues from existing integrated development environments (IDEs). Help development teams understand the impact of security threats with actionable insights and recommendations. 

SBOM management at scale
Support a chain of trust across the software life cycle. Provide signed attestation and detailed provenance of software components with an auto generated Software Bill of Materials (SBOM) for each run of the CI/CD pipeline.

Tamper-proof cryptographic signing
Ensure integrity of software artifacts at every step of the CI/CD workflow. Digitally sign and account for every code submission through a transparent, immutable open source log of all activities.

Security-focused automated workflows
Verify compliance standards, including Supply chain Levels for Software Artifacts (SLSA) Level 3. Implement user configurable approval gates with vulnerability scanning and policy checking for traceability and visibility.

Red Hat Trusted Application Pipeline includes:
Red Hat Developer Hub logo
Red Hat Developer Hub is an open framework for building internal developer platforms.

Learn more
Red Hat Trusted Profile Analyzer logo
Red Hat Trusted Profile Analyzer provides visibility into the risk profile of an application’s codebase.

Learn more
Red Hat Trusted Artifact Signer logo
Red Hat Trusted Artifact Signer protects the authenticity and integrity of software artifacts.

Learn more
Red Hat Security spot illustration 
Continuous, trusted software releases
Competitive organizations face the challenge of balancing speed and security as they build and release software. Security checks are necessary to stop bad actors from inserting malicious code or exploiting known vulnerabilities. But in complex and fast-moving software development life cycles, development teams don’t always have the time and tools to manually review every component.

Red Hat Trusted Application Pipeline improves the trust and transparency of the CI/CD pipelines, with security-focused golden paths that ensure software adheres to corporate standards. With integrated security checks, software teams can catch vulnerabilities early in the life cycle, delivering valuable new software at scale while improving resiliency and safeguarding user trust.




Securing your software supply chain is critical to prevent software vulnerabilities. Red Hat Trusted Application Pipeline embeds security throughout the software development lifecycle (SDLC), enabling teams to innovate confidently while adhering to the highest security standards.

1. Overview
RHTAP is a DevSecOps framework that integrates security from project inception to production. It incorporates advanced security practices to ensures that your software is resilient to threats while streamlining development processes.

1.1. Key features
Secure CI/CD pipelines: Build, test, and deploy container images securely using pre-configured pipelines integrated with your Git repository.

Ready-to-use templates: Start project quickly with customizable templates that apply secure development practices.

Vulnerability management: Detect and address potential vulnerabilities with detailed insights, including automated generation of Software Bills of Materials (SBOMs).

Compliance with Enterprise Contracts: Maintain regulatory compliance at every stage of the development process with our robust enforcement of security and quality standards.

1.2. Integrated technologies
RHTAP integrates with industry-leading platforms and tools:

Component or Technology	Description
Red Hat Developer Hub (RHDH)

A self-service portal that streamlines development and integrates security best practices from the get-go.

Red Hat Trusted Artifact Signer (RHTAS)

Enhances software integrity through signature and attestation, ensuring all artifacts are secure and authentic.

Red Hat Trusted Profile Analyzer (RHTPA)

Automates the creation and management of SBOMs, providing transparency and compliance in your software supply chain.

Advanced Cluster Security (ACS)

Automates the scanning of artifacts for vulnerabilities.

OpenShift GitOps

Manages Kubernetes deployments and infrastructure using Git repositories, ensuring consistent, automated, and secure deployment practices.

OpenShift Pipelines

Automates the CI/CD processes with visibility and control over build, test, and deployment workflows.

Argo CD

Automates application deployment and lifecycle management, ensuring consistent versions of app definitions, configurations, and environments.

1.3. Configuration options
RHTAP allows flexibility in CI/CD management, source repositories, and artifact registries:

Category	Options
CI/CD pipelines

Tekton (Default)

Jenkins

GitHub Actions

Gitlab CI

Note
All CI pipelines expect Tekton conform to SLSA Build L2. Tekton conforms to Build L3.
Source repositories

GitHub (Default)

GitLab

Bitbucket

Artifact registries

Quay (Default)

JFrog Artifactory

2. Development workflow
RHTAP integrates security at every step of the DevSecOps workflow:

Start with secure templates: Leverage pre-built templates from Red Hat Developer Hub (RHDH) for a secure foundation. These templates include code repositories, documentation, and pre-configured CI/CD pipelines.

Develop and modify code: Modify your code after creating the application. Each code change triggers a pipeline run that automatically performs security checks, including artifact signing, vulnerability scanning, and SBOM generation.

Managed deployment: RHTAP enforces security policies throughout the development lifecycle, from development to production, using Enterprise Contracts (EC). This ensures that only compliant builds are deployed.
