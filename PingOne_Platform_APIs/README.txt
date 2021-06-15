PingOne is a cloud-based identity as a service (IDaaS) framework for secure identity access management. The PingOne API gives developers the tools to manage users and integrate enterprise and third-party applications with the PingOne identity and application management platform.

This document describes the PingOne Management API services, which are used to manage your organization's users and applications, and the Authentication API services, which are used to manage authorization, authentication, permissions, and the sign-on policies that grant users access to applications.

The PingOne APIs manage access to your organization's applications and ensure that only authorized users (your customers, employees, and partners) have access to the applications they have permission to use.

Visit our docs page for a [Getting Started guide](https://apidocs.pingidentity.com/pingone/platform/v1/api/#getting-started) and some [Quick Start Tasks](https://apidocs.pingidentity.com/pingone/platform/v1/api/#quick-start-tasks) to get you familiar with our platform.

The collection includes an environment with several environment variables to streamline your process. Here are some of the commonly used ones and their descriptions.
	
|Postman variable| PingOne resource|
|-------------| ----------------|
|`accessToken` | A valid access token returned by the PingOne authorization server.|
|`actionID` | The UUID of a sign-on flow action resource. Action IDs are associated with the `/environments/{environmentId}/signOnPolicies/{policyId}/actions` endpoint to identify specific sign-on policy actions such as `Single_Factor` or `Multi_Factor`. |
|`activityID` | The UUID of an audit activity resource. Activity IDs are associated with the `/environments/{id}/activities/` endpoint, and they identify specific audit event actions, such as `APPLICATION.DELETED`.|
|`apiPath` | The regional domain for the PingOne server. These IDs identify a specific configured application in PingOne. Options are: `https://api.pingone.com/v1` for environments the North America region and `https://api.pingone.eu/v1` for environments in the European Union region. |
|`appID` | The UUID of an application resource. These IDs identify a specific configured application in PingOne. The `appID` is used to associate OIDC or SAML connection settings with the application specified by its UUID. |
|`appSecret` | The value of the application secret. This ID has a minimum length of 64 characters per SHA-512 requirements when using the HS512 algorithm to sign ID tokens using the secret as the key. |
|`attributeID` | The UUID of a custom attribute resource. Attribute IDs are associated with the `/environments/{environmentId}/schemas/{schemaId}/attributes/` endpoint to identify custom schema attributes.|
|`certID` | The UUID of a certificate resource.  Certificate IDs are associated with the `/environments/{environmentId}/certificates` endpoint to identify uploaded customer-provided certificates.|
|`subscriptionID` | The UUID of a subscription resource. Subscription IDs are associated with the `/environments/{environmentId}/subscriptions` endpoint to identify uploaded subscriptions.|
|`contentID` | The UUID of a content resource. Content IDs are associated with the `/environments/{environmentId}/templates/{templateName}/contents` endpoint to identify specific email or SMS notifications content. |
|`deviceID` | The UUID of a device resource. Device IDs are associated with the `/environments/{environmentId}/users/{userId}/devices` endpoint to associate devices with users for use in multi-factor sign-on actions. |
|`envID` | The UUID of an environment resource. This ID identifies your current working domain within your organization. Nearly all Management and Authentication API endpoints require an environment ID. |
|`grantID` | The UUID of authorization grant resource. Grant IDs are associated with the `/environments/{environmentId}/resources/{resourceId}/grants` endpoint to identify authorization grant types. Grant IDs are also used with the `/environments/{environmentId}/applications/{appId}/grants ` endpoint to associate resource grants with applications.|
|`imgID` | The UUID of an image resource.  Image IDs are associated with the `/environments/{environmentId}/images` endpoint to associated custom image files with the specified environment resource, which can be used for custom branding of the PingOne admin UI. |
|`keyID` | The UUID of an encryption key resource. Key IDs are associated with the `/environments/{environmentId}/keys` endpoint to identify uploaded customer-provided signing/encryption keys.|
|`passwordPolicyID` | The UUID of a password policy resource. Password policy IDs are used with the `/environments/{environmentId}/passwordPolicies` endpoint to associate password policies with the specified environment.|
|`policyID` | The UUID of a sign-on policy resource. Sign-on policy IDs are used with the `/environments/{environmentId}/signOnPolicies` endpoint to associate sign-on policies with the specified environment.|
|`popID` | The UUID of a population resource. Population IDs are used with the `/environments/{environmentId}/populations` endpoint to manage the populations to which users can be assigned. |
|`resourceID` | The UUID of a protected endpoint resource. Resource IDs identify the protected endpoints that applications request access to using OAuth 2 or SAML authorization protocols. These IDs are associated with the `/environments/{environmentId}/resources` endpoint.|
|`roleAssignmentID` | The UUID of a role assignment resource. These IDs are used with the `environments/{environmentId}/{actorType}/{actorId}/roleAssignments` endpoint to identify the roles assigned to a specified actor.|
|`roleID` | The UUID of a role resource. Role IDs are used with the `/roles` endpoint to identify platform roles defined in PingOne. Note that roles and role IDs are not associated with a specific environment.|
|`schemaID` | The UUID of a schema resource. Schema IDs are associated with the `/environments/{environmentId}/schemas` endpoint to identify custom user schema resources.|
|`scopeID` | The UUID of a scope resource. Scope IDs are used with the `/environments/{environmentId}/resources/{resourceId}/scopes` endpoint to define the scopes associated with a resource access grant.|
|`SOPAssignmentID` | The UUID of a sign-on policy assignment resource. These IDs are used with the `/environments/{environmentId}/applications/{applicationId}/signOnPolicyAssignments` endpoint to assign sign-on policies to the specified application.|
|`templateName` | The name of a notifications template task resource. These names are used with the `/environments/{environmentId}/templates` endpoint to identify a specific notifications template, which is used as the container for delivering notifications content to users. Options are: `offline_pairing`, `verification_code_template`, `recovery_code_template`, and `offline_authentication`.|
|`userID` | The UUID of a user resource. User IDs are used with the `/environments/{environmentId}/users` endpoint to identify specific user resources and manage user attributes.|