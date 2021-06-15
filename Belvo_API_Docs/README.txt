# Introduction
Belvo is an open banking API for Latin America that allows companies to access banking and fiscal information in a secure as well as agile way.
Through our API, you can access:

  - **Bank and Gig information** such as account statements, real-time balance, historical transactions, and account owner identification.
  - **Fiscal information** such as received and sent invoices and tax returns.

In this API reference you'll find all the information you need about each endpoint and resource. 

▶️ Make sure that you also check out our Developer Portal for guides on [how to get started](https://developers.belvo.com/docs/get-started-in-5-minutes), using our [Sandbox environment](https://developers.belvo.com/docs/test-in-sandbox), as well as how to [integrate the widget](https://developers.belvo.com/docs/connect-widget) or use our [quickstart application](https://developers.belvo.com/docs/quickstart-application).

  ## Environment
  We currently offer to environments: sandbox and production.

  | Environment | Purpose | Base URL |
  |-----------|-------|-------|
  | **Sandbox** | The [Sandbox environment](https://developers.belvo.com/docs/test-in-sandbox) is dedicated for your testing and development phases. In this environment, you can create links without real credentials and you can pull test data from all endpoints. **⚠️The sandbox environment is refreshed frequently and your test data can be updated or deleted.** | https://sandbox.belvo.com/ |
|**Development**|The Development environment is dedicated for testing with real credentials and institutions with real-world institutions. You can create up to 25 links for free in this environment.| https://development.belvo.com/ |
  | **Production** | The Production environment is dedicated for live applications with real connections to institutions. In this environment, you will need real credentials to create links and you will pull real data from the institutions.| https://api.belvo.com/ |

  For each environment, you'll need to [generate separate API keys](https://developers.belvo.com/docs/get-your-belvo-api-keys).

  ## Response codes

  We use the following HTTP status code in the response depending on the success or failure:

  | Status Code | Description |
  |-----------|-------|
  | `200` | ✅ **Success** - The content is available in the response body. |
  | `201` | ✅ **Success** - The content was created successfully on Belvo. |
  | `204` | ✅ **Success** - No content to return. |
  | `400` | ❌ **Bad Request Error** - Request returned an error, detail in content.|
  | `401` | ❌ **Unauthorized** - The Belvo credentials provided are not valid.|
  | `404` | ❌ **Not Found** - The resource you try to access cannot be found.|
  | `405` | ❌ **Method Not Allowed** - The HTTP method you are using is not accepted for this resource.|
  | `408` | ❌ **Request Timeout** - The request timed out and was terminated by the server.|
  | `428` | ❌ **MFA Token Required** - MFA token was required by the institution to connect. |
  | `500` | ❌ **Internal Server Error** - The detail of the error is available in the response body.|

  ## Error handling

  ### Error messages

  Belvo API errors are returned in JSON format. For example, an error might look like this:

  ```
  [
    {
      "request_id": "a6e1c493d7a29d91aed4338e6fcf077d",
      "message": "This field is required.",
      "code": "required",
      "field": "link"
    }
  ]
  ```

  Typically, an error response will have the following parameters:
  - `request_id`: a unique ID for the request, you should share it with the Belvo support team for investigations.
  - `message`: human-readable description of the error.
  - `code`: a unique code for the error. Check the table below to see how to handle each error code.
  - `field` *(optional)*: The specific field in the request body that has an issue.


  ### Request identifier
  When you need help with a specific error, add the request identifier (`request_id`) in your message to the Belvo support team. This will speed up investigations and get you back up and running in no time at all.

  ### Error codes and troubleshooting

  For a full list of errors and how to troubleshoot them, please see our dedicated [Error handling articles](https://developers.belvo.com/docs/integration-overview#error-handling) in our DevPortal.

  
  ### Retry policy
  
  Please see our recommended [retry policies](https://developers.belvo.com/docs/integration-overview#error-retry-policy) in the DevPortal.


Contact Support:
 Name: Need help?
 Email: support@belvo.com