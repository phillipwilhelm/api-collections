The Salesforce APIs collection contains 230+ requests for the following Salesforce APIs:

<table>
   <tr>
      <td>Async Query
          Auth
          Bulk (v1 & v2)
          Composite
          Connect (Chatter)
          CPQ</td>
      <td>Einstein Prediction Service
          Metadata
          Rest
          Tooling
          UI</td>
   </tr>
</table>

**⚠️ Disclaimers:**
- This collection is provided as-is. It's not officially supported by Salesforce or covered by SLAs.
- API documentation is not provided with the collection. Please refer to the [official documentation](https://developer.salesforce.com/docs).

ℹ️ Report issues and ask questions [here](https://github.com/forcedotcom/postman-salesforce-apis/issues).

## Get started

Follow [this documentation](https://github.com/forcedotcom/postman-salesforce-apis) to get started with the collection.

## Variables Reference

The collection relies on the following variables:

| Variable | Description |
| --- | --- |
| `url` | The base URL for all requests. Either:<br/>- `https://test.salesforce.com` for sandboxes or Scratch orgs<br/>- `https://login.salesforce.com` for production, Trailhead Playground and Developer Edition orgs<br/>- your custom My Domain base URL. |
| `version` | The Salesforce API version (e.g.: 50.0). |
| `username ` | Your username. |
| `password ` | Your password. |
| `secretToken ` | Your personal [security token](https://help.salesforce.com/articleView?id=user_security_token.htm). |
| `clientId ` | Connected App client Id. |
| `clientSecret ` | Connected App client secret. |
| `redirectUrl ` | Connected App redirect URL for OAuth 2.0. |
| `initAccessToken ` | Initial access token for dynamic Connected App registration. |
| `site ` | Community suffix when connecting with an Experience Cloud user. |

Only a few of these variables are mandatory. The authentication requests will automatically register and set extra "private" variables identified with a `_` prefix (e.g.: `_accessToken`, `_endpoint`, `_orgId`, `_userId`...).