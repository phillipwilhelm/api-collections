# Shopper Login and API Access Service (SLAS) Use Case Scenarios Using Postman
This Postman collection contains 6 use cases that SLAS supports. This collection will show how to get an authorization code, access token, create a shopper basket, place an item in the basket, and then delete the basket using a private SLAS client and a SLAS public client.

This collection was developed so that multiple SLAS deployments could be used by this collection simply by setting up different Postman environments.

For the registered user flow using a private client that is federated to a 3rd party IDP (like Okta, or Google) the IPD will need to be called from a browser to login and get an authentication code.

For the Proof Key for Code Exchange (PKCE) flows the `CODE_CHALLENGE` and `CODE_VERIFIER` will be created and stored as collection variables when using the tests that need them.

**⚠️ Disclaimers:**
- This collection is provided as-is. It's not officially supported by Salesforce or covered by SLAs.
- API documentation is not provided with the collection. Please refer to the [official documentation](https://developer.commercecloud.com/s/api-details/a003k00000VzoEyAAJ/commerce-cloud-developer-centershopperloginandapiaccessadmin).

ℹ️ Report issues and ask questions [here](https://github.com/forcedotcom/postman-commerce-cloud-apis/issues).

## Get started

Follow [this startup guide](https://github.com/forcedotcom/postman-commerce-cloud-apis) to get started with the collection.

## The 6 Use Cases
* **Guest User • Private Client** - Creates a SLAS JSON Web Token (JWT) using a SLAS private client id and secret in a authorization header.
* **Guest User • Public Client** - Creates a SLAS (JWT) using a PKCE flow using a code challenge, code verifier and a SLAS public user client id. An authorization header is not needed as the client id, without a secret is provider as a query parameter.
* **Ecom Registered User • Private Client** - Creates a SLAS JWT using Ecom customer credentials, code challenge, code verifier with a SLAS private client id and secret.
* **Ecom Public Registered User • Public Client** - Creates a SLAS JWT using the PKCE flow using Ecom customer credentials, code challenge, code verifier and a SLAS public client id.
* **Registered User • Private Client** - Creates a SLAS JWT using a 3rd party identity provider (IDP) with a SLAS private client id and secret.
NOTE: The IDP will need to be called from the browser and get an authorization code to be used for the SLAS `/token` endpoint.
* **Registered User • Public Client** - Creates a SLAS JWT using the PKCE flow and a SLAS public client id.

## Prerequisites
SLAS Use Case collection should have a SLAS service deployed and running and a Salesforce Commerce Cloud (ECOM) environment running. During SLAS service and ECOM setup a tenant id, private client id and secret, and a public client id should be set up. There also needs to be an active ECOM customer (shopper) with password that can be used with this collection.

## Variables Reference
The following variables should be setup as Postman environment variables before running any tests.

Related Environment: Salesforce Commerce Cloud SLAS Use Cases - Template

| Variable | Description |
| --- | --- |
| `host` | The host to the SLAS service. Should include the `https://` protocol. |
| `tenant_id` | The tenant id that was created when SLAS and ECOM was set up. |
| `base_uri` | The base URI to SLAS. ex. `/api/v1/organizations/` |
| `ocapi_uri` | The URI to ECOM to access the OCAPI APIs. Should include the `https://` protocol. |
| `ocapi_site` | The ECOM Site used in OCAPI calls. Ex. `SiteGenesis` or `RefArch` |
| `ecom_customer_id` | A customer (shopper) user from ECOM. |
| `ecom_customer_pw` | A customer (shopper) user password from ECOM. |
| `private_client_id` | The private client when client was created in SLAS. |
| `private_client_secret` | The private client secret when client was created in SLAS. |
| `public_client_id` | The public client when client was created in SLAS. |
| `redirect_url` | One of the `redirect_uris` that are part of the SLAS client. |

## Shopping Baskets
After each SLAS authorization there are tests to create a basket, add an item to the basket, get the basket and delete the basket. The basket id is saved during the tests so it can be used by the other tests. However, in the Add Item to basket test there is an ECOM product id in the body of the request. The product is based on the ECOM site that is chosen. The product id in the body may need to change to a product id in ECOM.