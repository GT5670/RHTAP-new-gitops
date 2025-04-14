:_newdoc-version: 2.18.3
:_template-generated: 2025-04-14
:_mod-docs-content-type: PROCEDURE

[id="integrating-azure-pipelines_{context}"]
= Integrating Azure Pipelines

If you want to integrate Azure with {ProductName}, complete the steps in the following procedure.

.Prerequisites

* You must have the necessary permissions in your Azure subscription to register applications and manage API permissions.

* You must register a personal access token (PAT). For detailed steps, see https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops[How to generate personal access tokens in Azure DevOps].


* You must collect the following values:

** `AZURE_ORGANIZATION`: The name of your Azure DevOps organization. For example, `my-org-name`.

** `AZURE_HOST_URL`: The base URL of your Azure DevOps environment. The default is `dev.azure.com`.

* Optional values, required only if you authenticate using a registered Azure Active Directory (AAD) application:

** `AZURE_TENANT_ID`: The Directory (tenant) ID. See https://learn.microsoft.com/en-us/partner-center/find-ids-and-domain-names[Find your tenant ID].

** `AZURE_CLIENT_ID`: The Application (client) ID. See https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app[Register an application with the Microsoft identity platform].

** `AZURE_CLIENT_SECRET`: The client secret generated in the AAD app. See https://learn.microsoft.com/en-us/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps#create-a-client-secret[Create a client secret].

.Procedure

. In your `rhtap-cli` container, run the integration command after replacing the placeholder values with your Azure DevOps credentials. Additionally, if you are using the default host (`https://dev.azure.com`), you can omit the `--host` option.
+
[source,bash]
----
bash-5.1$ rhtap-cli integration azure \
  --organization="$AZURE_ORGANIZATION" \
  --host="$AZURE_HOST_URL" \
  --token="$AZURE_API_TOKEN" \
  // Append only if you are using Microsoft authentication
  --tenantID="$AZURE_TENANT_ID" \
  --client-id="$AZURE_CLIENT_ID" \
  --client-secret="$AZURE_CLIENT_SECRET"
----
