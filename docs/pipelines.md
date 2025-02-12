.Prerequisites

* You must have admin access to your GitLab repository and CI/CD settings.

* You must have the credentials for your container registry to and pull container images, such as Quay.io, Jfrog Artifactory, or Sonatype Nexus. 

* You must have the following information for specific tasks that you want the GitLab CI to perform:

** For ACS tasks:

*** ROX Central server endpoint and token

** For SBOM tasks:

*** Cosign signing keys password, private key, and public key

*** Trustification URL, client ID, secret, and supported CycloneDX version
