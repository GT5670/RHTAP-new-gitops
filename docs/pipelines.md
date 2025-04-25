= About Red Hat Developer Hub

Red Hat Developer Hub (RHDH) is an enterprise-grade Internal Developer Portal (IDP) that simplifies and accelerates software development within organizations. It provides a customizable developer portal that integrates with Red Hat OpenShift and other cloud-native technologies to create a consistent environment for building, deploying, and managing applications.

RHDH acts as a central platform where development teams access source code repositories, CI/CD pipelines, APIs, and technical documentation. By integrating these tools and services, Red Hat Developer Hub establishes "golden paths" – predefined, best-practice workflows that guide developers through common tasks efficiently.

The outcome is increased developer productivity and satisfaction: engineers spend less time searching for resources or configuring infrastructure and more time writing high-quality code that meets enterprise standards.

== Understanding Internal Developer Platforms (IDPs)

An Internal Developer Platform is a curated set of integrated tools and services that provides a self-service platform for software developers within an organization. Rather than requiring developers to navigate multiple systems manually (source control, CI/CD, environments, monitoring), an IDP offers a streamlined experience where these systems are coordinated by a dedicated platform team.

The platform team configures automation and default "golden path" configurations for common tasks (such as creating a microservice or provisioning an environment), which developers can use with minimal effort through a portal, CLI, or APIs. The IDP removes repetitive setup work without hiding necessary context, balancing convenience with transparency.

=== Why IDPs matter

Internal Developer Platforms address the complexity of modern cloud-native development through:

* *Self-service capabilities*: Developers complete recurring tasks through self-service interfaces instead of filing tickets. Automation reduces manual errors and accelerates the development lifecycle.

* *Standardized workflows*: The platform includes pre-approved technology stacks, configurations, and processes that follow best practices. These "golden paths" ensure all projects meet organizational standards for security, compliance, and reliability.

* *Consolidated knowledge*: The developer portal serves as the primary source for discovering internal APIs, services, and documentation. This breaks down information silos by centralizing content previously scattered across wikis, ticket systems, and team repositories.

* *Enhanced developer experience*: By reducing cognitive load and providing a coherent interface, an IDP allows developers to focus on coding and solving business problems rather than managing infrastructure. This leads to faster onboarding and increased engineering productivity.

== Key features of Red Hat Developer Hub

Red Hat Developer Hub includes features designed to streamline the entire development process:

=== Centralized dashboard

RHDH provides a unified interface for accessing developer tools, CI/CD pipelines, APIs, monitoring tools, and documentation. It integrates with Git repositories, OpenShift, Kubernetes, and project management tools to deliver a comprehensive view of your development ecosystem.

=== Software catalog

The software catalog functions as the central inventory of all software assets, including services, applications, libraries, data pipelines, and APIs. It aggregates metadata from various sources into a searchable registry.

Benefits of the software catalog include:

* *Simplified discovery*: Find existing services, APIs, and libraries through direct search
* *Clear ownership information*: Identify who owns and maintains each component
* *Consistent metadata*: Access standardized information across all entries
* *Comprehensive search*: Locate related code, documentation, and infrastructure from one interface

For more information on software catalog see, link:/en/documentation/red_hat_developer_hub/1.5/html/about_red_hat_developer_hub/software-catalog[About software catalog]

=== Software templates

Software templates in RHDH provide on-demand scaffolding for new projects, eliminating the time-consuming and error-prone process of creating applications from scratch. These templates generate project repositories with all necessary configuration and boilerplate code.

Software templates provide:

* *Rapid project initialization*: Create new projects with appropriate structure and integrations in minutes
* *Standardized implementation*: Ensure organizational standards are incorporated into every new project
* *Developer autonomy with guardrails*: Enable developers to create projects independently while following approved patterns
* *Specialized templates*: Start development of AI-enabled applications using purpose-built templates

For more information on software templates, see link:/en/documentation/red_hat_developer_hub/1.5/html/about_red_hat_developer_hub/software-templates[About software templates]

=== Technical documentation

Red Hat Developer Hub includes a built-in technical documentation feature that centralizes documentation and simplifies its creation, maintenance, and discovery.

Technical documentation in RHDH provides:

* *Centralized documentation access*: Find all documentation through one interface
* *Streamlined maintenance*: Write documentation in Markdown alongside code
* *Enhanced searchability*: Locate relevant documentation quickly through integrated search
* *Uniform structure*: Navigate documentation more easily through consistent formatting



=== Learning paths

RHDH offers learning paths that guide developers through tutorials, educational materials, and onboarding sequences directly within the portal.

Learning paths deliver:

* *Structured onboarding*: Help new team members become productive quickly
* *Guided learning*: Follow step-by-step instructions for platform features
* *AI technology adoption*: Access specialized content for implementing AI/ML technologies
* *Integrated resources*: Utilize both internal and Red Hat learning materials



=== Plugins and integrations

RHDH integrates with existing development tools and presents their information in a unified interface.

The plugin ecosystem provides:

* *Platform extensibility*: Add functionality through Red Hat-supported and verified plugins
* *Tool consolidation*: Reduce context switching between different systems
* *Non-disruptive updates*: Add or update plugins without service interruptions
* *Runtime environment integration*: Connect seamlessly with OpenShift and cloud services
* *Automation interfaces*: Enable advanced workflows through APIs and CLI tools

For more information on Plugins and integrations, see link:/en/documentation/red_hat_developer_hub/1.5/html/about_red_hat_developer_hub/plugins-integrations[About plugins and integrations]

=== Role-based access control

RHDH includes enterprise-grade role-based access control that can be customized to meet organizational security requirements.

== Benefits for different audiences

=== For developers

Red Hat Developer Hub optimizes the daily experience of software developers by consolidating tools and automating repetitive tasks:

==== Faster onboarding
RHDH accelerates the onboarding process for new team members. The centralized software catalog and comprehensive documentation help developers quickly understand the organizational software landscape. Learning paths provide structured guidance, while templates enable rapid creation of development environments and sample applications. This results in significantly faster productivity with new codebases or technologies.

==== Reduced cognitive load
RHDH consolidates critical development resources, including code repositories, build pipelines, test results, environments, and deployment statuses. This eliminates the need to manage multiple interfaces and credentials or search through disconnected systems. A single search can replace exploration across multiple tools, allowing developers to focus on problem-solving rather than locating resources.

==== Self-service capabilities with guardrails
RHDH enables developers to create applications, APIs, or environments through self-service interfaces. This autonomy eliminates waiting for other teams to perform initial setup while maintaining security through platform guardrails such as pre-approved templates and automated policy checks. Developers can innovate confidently, knowing that built-in best practices ensure compliance with organizational standards.

==== Consistent processes
RHDH standardizes development processes across teams. Services in the catalog follow a consistent format, and template-generated projects adhere to established best practices. This consistency enables developers to move between projects and find familiar structures and tooling, reducing time spent addressing preventable issues and improving software quality and reliability.

==== Enhanced collaboration
The hub serves as a central communication point between development, operations, and other stakeholders. Developers gain visibility into how their work connects to the broader organization. The catalog shows service consumption patterns, while documentation from other teams and company-wide announcements are accessible from the portal. This transparency eliminates silos and promotes unified development approaches.

==== Improved productivity and satisfaction
By removing friction from the development process, RHDH allows developers to focus on building features and solving problems. Developers report less frustration and reduced context-switching fatigue when using an internal developer portal. A professional, customized portal demonstrates organizational commitment to developer experience, positively impacting team morale and retention.

=== For platform engineers

RHDH equips platform teams with effective tools for creating and maintaining exceptional developer experiences:

==== Customizable platforms with curated tools
Platform engineers can build experiences tailored to organizational needs by selecting from verified plugins and integrations. The plugin architecture supports adding only essential components, preventing feature bloat while ensuring developers have appropriate tools available.

==== Centralized configuration management
RHDH maintains consistent configuration through centralized repositories. Updates can be synchronized across the platform, improving version control and ensuring environment consistency. This centralization reduces maintenance requirements and prevents configuration drift between projects.

==== Simplified governance
RHDH streamlines technology choice oversight and operational process management. Templates and catalog policies make implementing and enforcing standards more straightforward. Platform teams can guide development practices without creating bottlenecks, balancing governance requirements with developer productivity.

=== For organizations

At the organizational level, RHDH delivers strategic advantages:

==== Scalability for organizational growth
RHDH enables rapid onboarding of new teams and supports application growth while maintaining consistency. The architecture scales with organizational needs, ensuring all developers—whether ten or a thousand—access the same quality tools and services. This scalability is essential for growing organizations or those planning expansion.

==== Enterprise-grade security
RHDH protects systems and data through robust role-based access control customized to organizational requirements. The security model ensures appropriate resource access, reducing risk while enabling productivity. As a Red Hat product, it benefits from enterprise security practices and regular updates addressing emerging threats.

==== Operational efficiency
RHDH eliminates workflow bottlenecks and reduces cognitive demands on development teams. By streamlining processes and centralizing resources, organizations save time and money. Developers spend less time on administrative tasks and more time creating value, while standardized practices reduce errors and remediation costs, accelerating time-to-market and optimizing resource usage.

== Getting started with Red Hat Developer Hub

Transform your development experience with these steps:

1. link:/en/documentation/red_hat_developer_hub/1.5/html/installing_red_hat_developer_hub/requirements[Review system requirements]
2. link:/en/documentation/red_hat_developer_hub/1.5/html/installing_red_hat_developer_hub/index[Install Red Hat Developer Hub]
3. link:/en/documentation/red_hat_developer_hub/1.5/html/user_guides/index[Explore feature guides]
4. link:/en/documentation/red_hat_developer_hub/1.5/html/configuring_red_hat_developer_hub/index[Customize with plugins and integrations]


