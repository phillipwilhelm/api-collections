Forte’s REST API enables merchants and partners to perform a variety of powerful tasks such as creating and updating credit card, echeck, and scheduled transactions, securely managing customer and payment data, querying and tracking settlement information, and creating and submitting merchant applications for new Forte organizations and locations. Forte uses standard HTTP protocols within a PCI-compliant architecture that is simple to integrate.

----
# Getting Started
To begin using Forte's REST web services, complete the following steps:
1. Sign up for a Test Account.
2. Create your API Credentials.
3. Create your Authentication Headers.
4. Craft a call.
5. Test your calls.

----

# Step 1: Sign Up for a Test Account
If you are a merchant, navigate to the [Forte Developer's Test Account](https://www.forte.net/test-account-setup) sign-up page and enter your First Name, Last Name, Company Name, and Email address in the applicable fields. Forte uses this email address for verification purposes and as your Username for registering and signing into [Dex](https://login.forte.net/), Forte's newest payment processing portal. 

If you are a partner, contact [Forte's Sales Team](mailto:sales@forte.net) and request a partner sandbox account. Partner accounts in Dex have different permissions and different menu options.   

After you verify your email address, Forte sends you a Dex invitation email where you can register for a sandbox account. Dex registration requires a mobile phone number that can receive SMS messages for account verification. 

After registering and verifying your mobile number, Dex logs you in with your Organization ID. Your **Organization ID** represents a legal entity that can own multiple sub-organizations (for partners) or multiple locations (for merchants) as well as the customers, payment methods, and transactions that belong to those locations. Every request call made to the Forte REST API must contain the `organization_id` within the URI. 

Every Dex sandbox account also comes with a Location ID. Your **Location ID** represents locations, which are processing endpoints that merchant organizations use to initiate transactions (in Forte legacy applications like Virtual Terminal, locations were known as MIDs). Locations own all the transaction data including sensitive payment method data and tokens. **Tokens** are random, alpha-numeric strings that represent stored, encrypted data. Tokenization is a common practice in the payment industry to protect sensitive data.

> For questions or help with Dex registration or setup, contact [Forte Technical Support](mailto:Integration@forte.net) at 888-235-4635 option 5.

----

# Step 2: Create Your API Credentials
To begin integration with Forte's REST API, you first have to create your API authentication credentials. These include an API Access ID, which acts as your username, and an API Secure Key, which acts as a password. You will create and maintain these credentials in Dex.

Complete the following steps to generate your API Access ID and API Secure Key:
1. From your Google Chrome browser, log into your [Dex](https://login.forte.net/) Account.
2. Select **Developer** > **API Credentials** from the Dex Main Menu.
3. Click the **CREATE** button. The Create API Credentials screen displays.
4. Enter a name for this set of API credentials in the **Name** field.
5. Click the **CREATE NEW API KEY** button. The **API Access ID** and **API Secure Key** values display in their corresponding fields.
7. Click the **COPY** button next to the **API Access ID** and **API Secure Key** fields to record both of these newly generated values in a secure location to use in authenticating your REST API requests.

> Once you save your **API Secure Key**, you will not be able to see the value again. If you forget your **API Secure Key** or it becomes compromised, you will have to regenerate the value in Dex.

----

# Step 3: Create Your Authentication Headers
Requests to Forte's REST API must be authenticated using the `Authorization` header field and the custom header property, `X-Forte-Auth-Organization-Id`.

## The Authorization Header
Forte's REST web services rely on [Basic access authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) over HTTPS using the **API Access ID** and an **API Secure Key** as the username and password values. These unique values are combined with a colon and then encoded using the RFC2045-MIME variant of Base64. The encoded string is then added to the HTTP `Authorization` header. For example, if you created the following API credentials: <ul><li>**API Access ID** = `315c7649520edde96c5cbad59a5b265f`</li><li> **API Secure Key** = `c233f2958bd855d09d98397e74950640`</li></ul><br />The value of the `Authorization` header field would look like the following:

```html
Authorization=Basic MzE1Yzc2NDk1MjBlZGRlOTZjNWNiYWQ1OWE1YjI2NWY6YzIzM2YyOTU4YmQ4NTVkMDlkOTgzOTdlNzQ5NTA2NDA=
```
<br />
Several different online tools can help you create your `Authorization` header, such as Postman. You can also add Base64 encoding to HMAC requests to automatically convert the API Access ID and API Secure Key values into the encoded ASCII string. To do so, use the following code:

```csharp
Convert.ToBase64String(Encoding.Default.GetBytes(APIAccessID + ":" + APISecureKey)).Trim()
```

## The X-Forte-Auth-Organization-Id Header
The custom header property `X-Forte-Auth-Organization-Id` specifies at which organization Forte should authenticate the request. A partner can authenticate his or her Organization ID in the `X-Forte-Auth-Organization-Id` header property and then can access merchant sub-organizations by specifying the merchant Organization ID in the URI of the request.

## The Accept Header
Forte’s REST service supports [Content Negotiation](https://en.wikipedia.org/wiki/Content_negotiation) through the `Accept` header sent in the request call.

The default value for `Accept` headers is `application/json` which returns JSON responses. However, you can also use `application/xml` which returns XML responses.

## The Content-Type Header
The `Content-Type` header is only required for POST and PUT calls. Like the `Accept` header, the `Content-Type` header supports both `application/json` and `application/xml`. The default value for `Content-Type` headers is `application/json`.

## Putting it All Together
In summary, you must include the following headers for every POST and PUT request call made to the Forte REST API. For GET and DELETE request calls, the `Content-Type` header is optional:

<ul>
<li> Content-Type - This header is only required for POST and PUT calls. This field defaults to application/json, but also supports application/xml.
<li> Accept - Defaults to application/json, but also supports application/xml</li>
<li> X-Forte-Auth-Organization-Id - A custom header property that specifies at which organization Forte should authenticate the request (i.e., org_{AuthOrganizationID})</li>
<li> Authorization - The API Access ID and API Secure Key encoded using the RFC2045-MIME variant of Base64.</li>
</ul>

----

# Step 4: Craft a Call
The following sections detail everything you'll need to create a request call. The API Reference section lists and explains all the resources you can use and provides samples of common requests and responses.

## Base URI
When constructing a call, append the resource endpoint to the following base URIs in the specified environments:

| URI                              | Environment     |
| -------------------------------- |----------------:|
| https://sandbox.forte.net/api/v3 | Sandbox         |
| https://api.forte.net/v3         | Live      |

For example, to find a specific customer in Sandbox, you would append the customer endpoint /organizations/{organization_id}/locations/{location_id}/customers/{customer_token} to the base URI https://sandbox.forte.net/api/v3 and perform a GET call. The complete URI, https://sandbox.forte.net/api/v3/organizations/{organization_id}/locations/{location_id}/customers/{customer_token} will return all the customer data attached to that customer's token.

## ID Formatting
All resources in Forte’s REST API require object prefixing to identify the specific resource and aid in troubleshooting in the event of errors. The resource ID is created by combining the object prefix with a unique ID number or token. The following table displays the prefixing standards used by Forte:

| Object            | Prefix    | Example                     |
| ----------------- |:---------:| ---------------------------:|
| organizations | org_ + ID   | `org_200000`                |
| locations     | loc_ + ID   | `loc_100000`                |
| customers     | cst_ + Token| `cst_SoGUG6mcLUS1nVzYBIbk3g` |
| addresses     | add_ + Token| `add_jUYRwbRjKUWgswNrFpSdKg` |
| paymethods    | mth + Token | `mth_ymC20TMkHE-YmYxMt0UvMA` |
| transactions  | trn_ + GUID | `trn_55c98c85-d3e8-4230-85e9-21d7d522eec0` |
| fundings      | fnd_ + ID   | `fnd_ACH-0226-173C5` |
| settlements   | stl_ + GUID | `stl_51cf4633-1767-484f-8784-be76a4076791` |
| schedules     | sch_ + GUID | `sch_2e5770ae-c120-414f-ae8c-d065753567e7` |
| scheduleitems | sci_ + GUID | `sci_4690fbfb-0b77-4477-a066-2c07ca2e5a3c` |
| disputes      | dsp_ + ID   | `dsp_2365435-e4ae-4ff4-a91e-abd8kjjfjffffc` |
| applications  | app_ + ID   | `app_258741` |
| documents     | doc_ + ID   | `doc_3131dddgwef0gpV2eYlo5` |

## Supported Actions
Use the following HTTP verbs to perform an action on REST API resources:

| Action | HTTP Method | Description                     |
| ------ |:-----------:| ---------------------------:|
| Create | `POST`      | Creates the resource that corresponds to the data type defined in the endpoint. For example, making a `POST` call to the `transactions` URI creates a new transaction.            |
| Find   | `GET`       | Returns summary information for all the resources that match the provided query parameters. For example, performing a `GET` call to the `customers` URI returns all the customers associated with that specific merchant location. To return comprehensive/detailed information on a specific resource, provide the resource’s ID to the defined URI. For example, to find a specific customer associated with a merchant location, perform a `GET` call to the `customers` endpoint and include the `customer_token` parameter in the URI                |
| Update | `PUT`       | Modifies the existing resource for the provided URI. All `PUT` calls require the resource’s ID. |
| Delete | `DELETE`    | Deletes the existing resource for the provided URI. All `DELETE` calls require the resource’s ID. |

## Request Filters for General GET Requests
Forte REST web services support the following filtering parameters for `GET` requests without resource IDs (i.e., general resource searches). Use these search filters for all resources. 

> Some resources (e.g., `transactions` and `settlements`) may have additional filter parameters that you can use to narrow down your search results.

| Parameter        | Description                                                                                                       |
| ---------------- |:------------------------------------------------------------------------------------------------------------------:
| `orderby`        | <ul><li>Sets the order of the results during a search request</li><li>Uses the same fields accepted by the `resource_filters`</li><li>Can be followed by a space and one of the following values designating the order to use<ul><li>`asc` - ascending (default if not specified)</li><li>`desc` - descending</li></ul></li></ul>| 
| `page_size`      | <ul><li>Sets the number of records returned on a page during a search request</li><li>Accepts values between 50 and 10000</li><li>If no value is defined, this parameter uses the default value of 50</li></ul>| 
|`page_index`      | <ul><li>Sets the index of the page of results returned during a search request</li><li>Index starts at 0 (zero) and has no upper limit</li><li>The given value must be a positive number</li><li>An index number set to a value higher than the max page value in a search request will return empty search results</li></ul> |

When using search filters, the `search_criteria` object will display in the response and echo back all the resource parameters included in the search in the `resource_specific` object.

## Understanding Responses
Forte includes the applicable parameters of the `response` object in all response calls returned to the client that made the request. 

> Optional request parameters whose values are null do not echo back in responses. The following table displays the response object and the parameters returned for each resource request.

| Parameter           | Description                                                                                 | Type                      |
| ------------------- |:-------------------------------------------------------------------------------------------:| -------------------------:|
| `response_desc`     | A short description of the action's response. All resources use this parameter.             | string              |
| `environment`       | The environment in which the user made the request. The value for this field can be either `live` or `sandbox`. All resources use this parameter.| string|
| `authorization_code`| The code indicating whether or not the transaction was authorized. This field is not used for voiding transactions.| string` |
| `response_type`     | The type of response this action generated: <ul><li>`A` - Approved</li><li>`D` - Declined</li></ul>| string |
| `response_code`     | The [response](https://fortepayments.freshdesk.com/support/solutions/articles/11000070426-transaction-and-settlement-codes) code of the action. | string |
| `preauth_result`    | Pre-authorization check result from Forte Verify with the following possible values:<ul><li>`POS` - Positive</li><li>`NEG` - Negative</li><li>`UNK` - No information available</li></ul> | string |
| `preauth_desc`      | Pre-authorization check descriptoin from Forte Verify with the following possible values:<ul><li>`POS` - Positive</li><li>`NEG` - Negative</li><li>`UNK` - No information available</li></ul>   | string |
| `preauth_neg_report`| Negative database response information (unformatted) when `pg_preauth_result=NEG`. | string
| `avs_result`        | Forte only returns this field if the merchant passes any combination of billing address parameters from the `physical_address object` in the request. To test this service in `Sandbox`, see the testing parameters in the [Verifying Credit Cards](https://fortepayments.freshdesk.com/support/solutions/articles/11000070558-verifying-credit-cards) tutorial and [Response Codes](https://fortepayments.freshdesk.com/support/solutions/articles/11000070426-transaction-and-settlement-codes) section. Supported values for this field include the following: <ul><li> `X` - Match: Street address and 9-digit zip code both match</li><li> `Y` = Match: Street address and 5-digit zip code both match</li><li> `A` = Partial Match: Street address matches, but both 5-digit and 9-digit zip code do not match</li><li> `W` = Partial Match: Street address does not match, but 9-digit zip code matches</li><li> `Z` = Partial Match: Street address does not match, but 5-digit zip code matches</li><li> `N` = No Match: Street address, 5-digit zip code, and 9-digit zip code all do not match</li><li> `U` = System unavailable: Address information unavailable. Forte returns this response if the street address is a non-US address, if the AVS service is unavailable, or if the AVS service for a particular US bank is not functioning properly</li><li> `R` = System unavailable: Forte will retry the AVS check because the issuer's system is unavailable or the request times out</li><li> `E` = Invalid: AVS data is invalid</li><li> `S` = Not supported: The US issuing bank does not support AVS checks</li></ul> | string |
| `cvv_result` | The card verification value response. Supported values for this field include the following: <ul><li> `M` = Match</li><li> `N` = No Match</li><li> `E` = Error (Unrecognized or Unknown Response)</li><li> `I` = Invalid or Null</li><li> `P` = Not Processed</li><li> `S` = Service Not Supported</li><li> `U` = Issuer Unable to Process</li><li> `X` = No Response</li></ul> |string |
| `available_card_balance`      | The available balance on the credit card if a credit card is used for the transaction.    | string |
| `requested_amount`  | The transaction amount   | string |

### Hypermedia
Forte’s REST API returns the following format for hypermedia responses. Result availability depends on the resource/action in the request. 

> The following sample of hypermedia responses are merely formatting examples provided for reference.

```json
{
   "links": {
     "self":"/customers?page_index=1",
     "prev":"/customers?page_index=0",
     "next":"/customers?page_index=2",
     "paymethod":"/customers/cst_SoGUG6mcLUS1nVzYBIbk3g/paymethods",
     "transactions":"/customers/cst_SoGUG6mcLUS1nVzYBIbk3g/transactions",
     "addresses":"/customers/cst_SoGUG6mcLUS1nVzYBIbk3g/addresses",
   }
}
```

### Status Codes
Forte's web services use standard HTTP status codes along with messages where appropriate. The table below displays the most common codes:

| Code  | Text                             | Description                     |
| ------|:--------------------------------:| ---------------------------:|
| `200` | OK                               | This code indicates a successful HTTP request; the actual response depends on the request method. For example, responses for `GET` requests contain entities corresponding to the requested resource while responses for `POST` requests contain entities describing the result of the action.|
| `201` | Created                          | This code indicates that the server has fulfilled the request and has created a new resource.|
| `400` | Bad Request or Failed Transaction| This code indicates that the server cannot fulfill the request because of bad syntax (e.g., a create echeck request with a missing routing number) or the transaction failed (responses for failed transactions also contain the failed transaction information).|
| `401` | Unauthorized                     | This code occurs when the user sends a bad username, password, and X-Forte-Auth-Organization-Id combination with the request.|
| `404` | Not Found                        | This code occurs when the user attempts an ID `GET` request, but the ID he/she provides does not exist in the database.|
| `500` | Internal Error                   | This generic error code indicates that the server has encountered an unexpected condition and cannot provide a more specific or suitable error message. |

For status codes in the 400s, ensure that you correctly formatted the JSON (or XML) in the original request, especially when the system returns a descriptive error message along with the status code such as the following example messages:

*Example 1*

```
{
    message: "Authentication Organization ID in header is missing or invalid."
}
```
<br />
*Example 2*

```
{
    message: "Payment Method's routing number length is invalid."
}
```


### Understanding Webhooks
Webhooks provide near-real-time notifications about the events that occur during a transaction through `POST`s to a customer-defined endpoint. Forte notifies merchants about events through subscriptions. Depending on these subscriptions, multiple events can occur during an operation. For example, a `POST` transaction request that creates tokens for a customer and a paymethod causes three events to be fired: `transaction.sale`, `customer.create`, and `paymethod.create`. These three events can be combined under a common event ID (e.g., `evt_xxxxxx`) for easier information management. 

> Depending on how you configure your event subscriptions, the same data may be generated twice in separate webhooks. For example, a `POST` to the `customer` object that includes the creation of a paymethod could (if subscribed) generate a customer webhook with both customer and paymethod data as well as a paymethod webhook. 

Merchants can subscribe to the following webhook events:
+ transaction.authorize
+ transaction.capture
+ transaction.credit
+ transaction.inquiry
+ transaction.sale
+ transaction.verify
+ transaction.void
+ customer.create
+ customer.update
+ customer.delete
+ paymethod.create
+ paymethod.update
+ paymethod.delete
+ schedule.create
+ schedule.update
+ schedule.delete

If a webhook post fails (i.e., does not result in an HTTP `200` response), Forte retries the webhook post up to twenty times adding one minute for each retry.

For more information on Webhooks, see [Using Webhooks](https://fortepayments.freshdesk.com/support/solutions/articles/11000070740-using-webhooks).

----

# Step 5: Test Your Calls
To help you gain a greater understanding of how Forte's REST API works, we've built a [Postman](https://www.getpostman.com/docs) collection of sample REST requests that you can use to test each resource. **NOTE**: While we've included sample body parameters in this collection of request calls, you'll still need to add the URLs and Authentication Headers described in Step 3 above.   

Postman maintains a thorough documentation repository. Use it to [set up your own environment](https://www.youtube.com/watch?v=wArvaHYdw2I&list=PLM-7VG-sgbtCJYpjQfmLCcJZ6Yd74oytQ&autoplay=1) and [create your own global variables](https://www.youtube.com/watch?v=TU1i1CgjVR8&list=PLM-7VG-sgbtCJYpjQfmLCcJZ6Yd74oytQ&index=2) to perform tests with your unique **Organization ID**, **Location ID**, **API Access ID**, and **API Secure Key**.

----

# Tokens
A token is a unique string ID that references stored customer information, including payment, customer, and address data. Tokens provide customers convenient, secure access to their information, making the checkout process faster and easier. For merchants, tokens provide a convenient method of collecting scheduled recurring payments. For more information on tokens, see the [Understanding Tokens](https://www.forte.net/devdocs/reference/tokens.htm#) tutorial on DevDocs. 

----

# Response Codes
For more information on response codes, see the [Transaction Codes](https://www.forte.net/devdocs/reference/transaction_response_codes.htm) page on DevDocs.

----

# Rate Limits
Forte throttles API requests to 10 per second. Once the request limit is met, Forte drops the connection and displays the following error: `403 - Forbidden: Access is denied`. For general synchronization of your transaction data, query the [settlements](https://restdocs.forte.net/?version=latest#8dcc3490-bc9c-4794-ba52-38bf25b924be) and [fundings](https://restdocs.forte.net/?version=latest#d1907bd8-046a-452d-812e-54a4e15f78b7) endpoints using strategic date and timestamp filters in the request.  Do not query individual transactions; this will bog down your connection and limit your payment processing ability. We recommend using single transaction queries on a limited basis for user-initiated, real-time status updates. For more information, see our blog post [here](https://blog.forte.net/tracking-settlement-and-funding-updates-with-smart-querying/).

------------

# Versions

| Version                              | Description     |
| -------------------------------- |----------------:|
| 1 | <ul> <li>Included only the following objects: <ul><li>Accounts</li> <li>Locations</li> <li>Customers</li> <li>Addresses</li> <li>Paymethods</li></ul></li> <li>Authentication done using an API Login ID and a Secure Transaction Key provided by Forte Integration Team.</li> <li>Only available in Sanbox.</li></ul>        |
| [2](https://www.forte.net/devdocs/api_resources/forte_api_v2.htm)       | <ul><li> Authentication using an API Access ID and an API Secure Key provided by Forte Integration Team.</li> <li> Enpoints using Account IDs and Location IDs.</li> <li> Available for both Sandbox and Live.</li></ul>      |
| [3](https://restdocs.forte.net/)  |<ul><li>Authentication using the API Access ID and API Secure Key that the developer creates in Dex.</li> <li>Endpoints now using Organization IDs and Location IDs.</li></ul>                             | 
