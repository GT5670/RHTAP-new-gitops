:_mod-docs-content-type: PROCEDURE

[id="integrating-acs_{context}"]
= Integrating ACS

.Prerequisites

* Administrator access to an instance of ACS

.Procedure

. Before you can integrate your instance of ACS, you need an API token and the central endpoint URL.
.. Follow the instructions for the prerequisites link:https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_security_for_kubernetes/{ACSVersion}/html/configuring/configure-api-token#create-api-token_configure-api-token[here] to create an API token. Save the token in `private.env`.
.. Follow the instructions link:https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_security_for_kubernetes/{ACSVersion}/html/configuring/configure-endpoints#configure-endpoints-existing_configure-endpoints[here] to configure your endpoint. Save the URL in `private.env`.

. In your `rhtap-cli` container, run the integration command. Replace $ACS_ENDPOINT with your ACS central endpoint URL, and $ACS_TOKEN with your ACS API token.
+
[source]
--
bash-5.1$ rhtap-cli integration acs --endpoint="$ACS_ENDPOINT" --token="$ACS_TOKEN"
--
