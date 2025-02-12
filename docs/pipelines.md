Before you configure GitLab CI, ensure you have the following:

* Admin access to your GitLab repository and CI/CD settings.

* Container registry credentials for pulling container images from Quay.io, JFrog Artifactory, or Sonatype Nexus.

* Authentication details for specific GitLab CI tasks:

** For ACS security tasks:

*** ROX Central server endpoint
*** ROX API token

** For SBOM and artifact signing tasks:

*** Cosign signing key password
*** Private key and public key
*** Trustification URL
*** Client ID and secret
*** Supported CycloneDX version

+
[NOTE]
====
The credentials and other details are already Base64-encoded, so you do not need to convert them. You can find these credentials in your `private.env` file, the file that you created at the time of installing {ProductShortName}. 
====
