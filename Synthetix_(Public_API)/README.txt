# Ahoy! Welcome aboard good ship Synthetix
The Synthetix Application Programming Platform or **SYNAPPS** is organized around REST. Our API has predictable, resource-oriented URLs, and error codes to indicate API errors. We use built-in HTTP features, like HTTP
headers and HTTP verbs, which are understood by off-the-shelf HTTP clients.

We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website's client-side code). JSON is returned by all API responses.

# Authentication
Access to all **SYNAPPS** resources require authentication with API `APPLICATIONKEY` and `CONSUMERKEY` keys. These are available only to registered and authorised users and have to be tied to a default view onto your knowledge base and product set.  Once a session has been initiated, however, the view can be updated.

Authenticate your account when using the API by including your API consumer and application keys in the head. You can manage your API keys in our control panel. Your API keys carry many privileges, so be sure to keep them secret! Do not share your secret API keys in publicly accessible areas such GitHub, client-side code, and so forth.

Authentication to the API is performed via HTTP Head. Provide your API consumer and application keys as the `APPLICATIONKEY` and `CONSUMERKEY` headers. You **do not** need to provide a password.

    {"APPLICATIONKEY": "XXXX515c765cd14604c86239147bXXXX", "CONSUMERKEY": "XXXXb1a10db65bd2d64cb5901be1XXXX"}

You have the ability to enforce origin access identity to restrict access so only your website or application can use your keys. This is to prevent unauthorised applications from using your key and consuming your quota or access your data. You can enforce origin access identity using a list of URLs or IPs within the Control Panel.

# Usage Quotas
Usage quotas are based on individual calls and are calculated per application. Not all resource calls are included in the quota calculation. We will provide usage quotas in accordance with your commercial arrangement and product set in use. Usage quotas are calculated on a monthly basis, and will reset on the first day of each new month. Should your application approach your usage quota, you will be notified in good time. Notifications will repeat regularly as you approach your limit. We are able to allow a small amount of overrun on a discretionary basis, subject to commercial arrangements, but we reserve the right to enforce and change individual application usage quotas, particularly if we perceive abuse.

# Rate Limiting
All of our resources are rate limited; this means that only allow a certain number of requests over a set period of time.  

| Environment | Authentication Type | Calls | Window
|--|--|--|--|
| Development | application-only | 100 | 1 minute
| Development | per-user | 600 | 1 minute
| Staging | application-only | 100 | 1 minute
| Staging | per-user | 600 | 1 minute
| Live | application-only | 100 |1 minute
| Live | per-user | 1200 | 1 minute

> *We reserve the right to adjust these limits at any time without further notice. Should you find your application exceeding your allocated rate limits, it is your responsibility to reduce your requests accordingly.*

## Per User or Per Application

Rate limiting of the standard API is primarily on a **per-user** basis — or more accurately described, per session. If a method allows for 100 requests per rate limit window, then it allows 100 requests per window per access token.

When using **application-only** authentication, rate limits are determined by IP address. If a method allows for 100 requests per rate limit window, then it allows you to make 100 requests per window — on behalf of your IP. This limit is considered completely separately from per-user limits.


## HTTP Headers and Response Codes
Use the HTTP headers in order to understand where the application is at for a given rate limit, on the method that was just utilised.

Note that the HTTP headers are contextual. When using **app-only** auth, they indicate the rate limit for the IP context. When using user-based auth, they indicate the rate limit for that user-application context.

When an application exceeds the rate limit all API calls from an app made after a rate limit is exceeded are throttled and will return a HTTP 429 “Too Many Requests” response code, and the following error will be returned in the response body:

    {
      "Error": 158,
      "Description": "RATE LIMIT EXCEEDED",
      "extraInfo": "The one-minute API limit of 100 requests has been exceeded. Please wait 60 seconds before attempting again. You are currently being throttled."
    }
    


# Sessions & Authorization Headers
Most SYNAPPS resources require a session to be initiated prior to proceeding. This can be identified by the small padlock icon next to a resource name. Successful initiation of a session will return an encrypted token that should be passed as a Bearer header for most of our resources. Session tokens enable us to enforce additional security on fundamental resources, pass encrypted information and allows logging and analysis of the activity of a specific user session. A session token must be generated for each unique user and will expire 2 hours after generation.

The endpoints that use sessions for authorization must set the session as an ['Bearer token'](https://swagger.io/docs/specification/authentication/bearer-authentication/) in the [authorization request header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#Authentication_schemes)  as seen in the example below:

    {"Authorization": "Bearer XXXX259A-6545-317D-ED45-1FA0DCFAXXXX"}


# Versioning And Change Logging
When we make changes to API resources, we document these on our  [Support page](https://support.synthetix.com)   and our [Twitter](https://twitter.com/SynthetixHelp). We recommend that all users of SYNAPPS resources subscribe to the support page and Twitter account to ensure they stay abreast of any updates. Deprecated resources will be retained but not updated.

Backwards incompatible changes to resources will trigger the release of a new version of the API. The release of a new version will be publicised in the documentation and on the Twitter feed.

# Restrictions And Limitations
You cannot interfere with, modify or disable any features, functionality or security controls of the SYNAPPS API resources and/or associated Synthetix services. You may not defeat, avoid, bypass, remove, deactivate or otherwise circumvent any protection mechanisms of the SYNAPPS API resources and/or associated Synthetix services. You may not reverse engineer, decompile, disassemble or derive source code, underlying ideas, algorithms, structure or organizational form from any SYNAPPS API resource and/or associated Synthetix service.

You are solely responsible (and Synthetix has no responsibility or liability of any kind), for the content, development, operation, or maintenance of your SYNAPPS applications. You will be solely responsible for the technical installation and operation of your SYNAPPS applications, for creating and displaying information and content on, through or within your SYNAPPs applications; for ensuring that your SYNAPPS applications do not violate or infringe the Intellectual Property Rights of any third party; and for ensuring that your SYNAPPS applications do not contain or introduce Malicious Software into the API, or any data stored and/or reported on using associated Synthetix services or transmitted using SYNAPPS API resources.

You must respect and comply with the technical and policy-implemented limitations of the API and the restrictions Synthetix designs or informs you of in accessing or using the API or designing and implementing SYNAPPS applications. Without limiting the foregoing, you may not violate any explicit rate limitations on calling or otherwise utilizing the API resources.

To the extent you develop or implement SYNAPPS applications that transmit or otherwise use or access the API to transmit data outside the Synthetix architecture, you will be responsible for any required notification to or consent of agents or end users that their data will be thus transmitted. Synthetix is not responsible for the privacy, security or integrity of data to the extent it is transmitted outside the Synthetix architecture by you or your applications using the SYNAPPS API resources.

# Channels
The different modalities of potential contact are designated 'channels'.  In most cases channel codes are not required, but for the avoidance of doubt channel codes are as found below.

| Channel Number | Description | Status |
|--|--|--|
| 0 | Live Chat | Active |
| 1 | Callback | Active |
| ~~2~~ | ~~Email~~ | Inactive |
| ~~3~~ | ~~voip~~ | Inactive |
| ~~4~~ | ~~Video~~ | Inactive |
| ~~5~~ | ~~WhatsApp~~ | Inactive |
| ~~6~~ | ~~Skype~~ | Inactive |
| ~~7~~ | ~~SMS~~ | Inactive |
| ~~8~~ | ~~Twitter~~ | Inactive |
| ~~9~~ | ~~Ticket~~ | Inactive |
| 10 | Facebook | Active |
| 14 | Knowledge | Active |
| 15 | IVA | Active |
| 16 | Form Agent | Active |
| 17 | Virtual Agent | Active |
| 99 | Unknown | Active |


# Error Codes
We use error codes to indicate any failure of an API request. **(Expand to view the full list)**.

You can also  ['**GET** .../helper/error'](#815f0c0f-5910-476f-8dca-e0467509f438) to get a list of error codes.

| Error Code/Number | Severity | Description | ['HTTP Status Code'](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) |
|--|--|--|--|
| 101 | NOTICE | NOT USING HTTPS 443 | 426 (Upgrade Required) |
| 102 | INFO | INVALID HEADERS | 406 (Not Acceptable) |
| 103 | INFO | API CALL QUOTA LIMIT EXCEEDED | 406 (Not Acceptable) |
| 104 | INFO | FORMAT MISSING | 200 (OK) |
| 105 | INFO | INVALID FORMAT | 405 (Method Not Allowed) |
| 106 | INFO | MISSING PARAMETER | 200 (OK) |
| 110 | INFO | APPLICATION OFFLINE | 423 (Locked) |
| 111 | INFO | BAD ORIGIN IP | 403 (Forbidden) |
| 112 | INFO | TOKEN DOES NOT CONTAIN VALID SIGNATURE | 200 (OK) |
| 113 | INFO | TOKEN EXPIRED | 401 (Unauthorized) |
| 114 | INFO | INVALID TOKEN | 401 (Unauthorized) |
| 115 | INFO | INVALID IP | 200 (OK) |
| 117 | INFO | DATA NOT VALID | 200 (OK) |
| 124 | CRITICAL | FAILED TO CONNECT | 503 (Service Unavailable) |
| 128 | INFO | HTTP PUT METHOD NOT AVAILABLE | 405 (Method Not Allowed) |
| 129 | INFO | HTTP HEAD METHOD NOT AVAILABLE | 405 (Method Not Allowed) |
| 130 | INFO | HTTP DELETE METHOD NOT AVAILABLE | 405 (Method Not Allowed) |
| 131 | INFO | HTTP OPTIONS  METHOD NOT AVAILABLE | 405 (Method Not Allowed) |
| 132 | INFO | HTTP GET  METHOD NOT AVAILABLE | 405 (Method Not Allowed) |
| 133 | INFO | HTTP OPTIONS POST NOT AVAILABLE | 200 (OK) |
| 134 | INFO | HTTP METHOD NOT ACCEPTED | 405 (Method Not Allowed) |
| 135 | INFO | MODE NOT RECOGNIZED | 200 (OK) |
| 136 | INFO | NO RESULTS | 200 (OK) |
| 137 | CRITICAL | CANNOT CONNECT | 503 (Service Unavailable) |
| 144 | CRITICAL | CANNOT CONNECT | 503 (Service Unavailable) |
| 145 | CRITICAL | CANNOT CONNECT | 503 (Service Unavailable) |
| 146 | INFO | INVALID CHANNEL | 501 (Not Implemented) |
| 147 | INFO | VOID ID | 200 (OK) |
| 148 | INFO | MISSING OR MALFORMED SKILL | 200 (OK) |
| 149 | INFO | INVALID SKILL | 200 (OK) |
| 150 | INFO | INVALID VARIABLE | 200 (OK) |
| 151 | INFO | 3RD PARTY RETURNED INVALID STATUS RESPONSE | 200 (OK) |
| 154 | INFO | NO DATA | 200 (OK) |
| 155 | INFO | CANNOT SET 3RD PARTY TIMEOUT | 200 (OK) |
| 156 | INFO | 3RD PARTY INTEGRATION SETTINGS INCOMPLETE | 200 (OK) |
| 157 | INFO | NO RESULTS | 200 (OK) |
| 158 | INFO | RATE LIMIT EXCEEDED | 429 (Too Many Requests) |
| 159 | INFO | MALFORMED TIME RATE PARAMETER | 200 (OK) |
| 160 | INFO | 3RD PARTY SESSION DOES NOT EXIST | 200 (OK) |
| 161 | INFO | 3RD PARTY ENVIRONMENT HAS A FAULT | 200 (OK) |
| 162 | INFO | NO RESULTS | 200 (OK) |
| 163 | INFO | NO SLA DATA | 200 (OK) |
| 164 | INFO | NO AUTO RESPONDER | 200 (OK) |
| 165 | INFO | CATEGORY DOES NOT EXIST | 200 (OK) |
| 166 | INFO | CATEGORY AND SUBCATEGORY ARE INCOMPATIBLE | 200 (OK) |
| 167 | INFO | CANNOT FIND GLOBAL PRESETS | 200 (OK) |
| 169 | INFO | INCOMPATIBLE PARAMETERS | 200 (OK) |
| 170 | INFO | NO ACCESS TO THIS RESOURCE | 403 (Forbidden) |
| 171 | INFO | CANNOT CHANGE EXISTING EMAIL | 200 (OK) |
| 173 | HIGH | CSRF SUSPECTED | 200 (OK) |
| 174 | INFO | ALREADY SUSPENDED | 200 (OK) |
| 175 | INFO | ALREADY UNSUSPENDED | 200 (OK) |
| 177 | INFO | VOID TRIGGER ID | 200 (OK) |
| 179 | INFO | UNKNOWN SUBDOMAIN | 200 (OK) |
| 180 | INFO | TEAM MATE INVALID | 200 (OK) |
| 181 | INFO | YOU ARE NOT A PARTICIPANT IN THIS CONVERSATION | 200 (OK) |
| 182 | INFO | CHAT NOT ASSIGNED TO YOU | 200 (OK) |
| 183 | INFO | ERROR IN UPDATING OR ADDING AD IMPRESSIONS | 200 (OK) |
| 184 | INFO | TRANSFER NOT AVAILABLE | 200 (OK) |
| 185 | WARNING | LOGGING FAILURE | 200 (OK) |
| 186 | WARNING | CANNOT REMOVE OWNER | 200 (OK) |
| 187 | INFO | MURDER, DEATH, KILL. OR (INVALID PARTICIPANT) | 200 (OK) |
| 188 | HIGH | DATABASE UPDATE ERROR | 200 (OK) |
| 189 | INFO | DUPLICATE CATEGORIES IN KNOWLEDGE BASE | 200 (OK) |
| 190 | INFO | AGENT IS INACTIVE | 200 (OK) |
| 191 | INFO | TITLE DOES NOT MEET LIMIT REQUIRMENTS | 200 (OK) |
| 192 | INFO | INVITATION ALREADY OFFERED | 200 (OK) |
| 193 | INFO | NO GOALS AVAILABLE | 200 (OK) |
| 194 | INFO | NO TOKEN OR SESSION IN PAYLOAD | 200 (OK) |
| 195 | INFO | API DOES NOT EXIST | 200 (OK) |
| 196 | INFO | YOUR SLOTS ARE FULL | 200 (OK) |
| 197 | INFO | PROBLEM WITH SUBMITTER | 200 (OK) |
| 198 | INFO | SKILL NO LONGER ACTIVE | 200 (OK) |
| 201 | INFO | MISSING APPLICATION KEY | 200 (OK) |
| 202 | INFO | MISSING CONSUMER KEY | 200 (OK) |
| 203 | INFO | ANTECEDING ENTITY IN QUEUE | 200 (OK) |
| 204 | INFO | NOT AUTHORISED | 403 (Forbidden) |
| 222 | INFO | NOT AUTHORISED | 200 (OK) |
| 223 | NOTICE | YOU HAVE NO PERMISSIONS | 200 (OK) |
| 224 | NOTICE | AGENT HAS NO MODULES | 200 (OK) |
| 225 | NOTICE | ACCOUNT IS LOCKED | 403 (Forbidden) |
| 226 | INFO | USER SET AS LOGGED OUT | 401 (Unauthorized) |
| 227 | INFO | CANNOT RETURN TO QUEUE IF INVITATION STILL OUT | 200 (OK) |
| 228 | HIGH | ONGOING CHATS AND DB OUT OF SYNC | 200 (OK) |
| 229 | INFO | TICKET DOES NOT EXIST | 200 (OK) |
| 230 | INFO | PERMISSION NOT SET | 401 (Unauthorized) |
| 231 | INFO | USERNAME INVALID | 200 (OK) |
| 232 | INFO | USERNAME ALREADY TAKEN | 200 (OK) |
| 233 | INFO | EMAIL INVALID | 200 (OK) |
| 234 | NOTICE | USER DOES NOT BELONG TO THIS AGENT | 200 (OK) |
| 235 | NOTICE | NO MFA METHOD | 200 (OK) |
| 236 | INFO | RESET SESSIONS | 200 (OK) |
| 237 | NOTICE | USER ID VOID | 200 (OK) |
| 238 | INFO | LABEL ID VOID | 200 (OK) |
| 239 | INFO | CHAT ALREADY COMPLETE | 200 (OK) |
| 240 | INFO | ONLY OWNERS CAN END CHATS | 200 (OK) |
| 241 | INFO | BAD SIGNATURE | 200 (OK) |
| 242 | INFO | HISTORICAL API CANNOT BE USED FOR REALTIME DATA | 200 (OK) |
| 243 | INFO | INVALID SCORE | 200 (OK) |
| 244 | INFO | TRIGGER ID INVALID FOR TYPE | 200 (OK) |
| 245 | INFO | INVALID REASON FOR SUSPENSION | 200 (OK) |
| 246 | INFO | PIPELINE NOT OWNED BY USER | 200 (OK) |
| 247 | INFO | PIPELINE DOES NOT EXIST | 200 (OK) |
| 248 | INFO | NO BREADCRUMBS COLLECTED | 200 (OK) |
| 249 | NOTICE | INVALID USER ID FOR THIS ACTION | 200 (OK) |
| 250 | INFO | CALLBACK ID NOT RECOGNISED | 200 (OK) |
| 251 | INFO | CALLBACK ALREADY COMPLETE | 200 (OK) |
| 252 | INFO | CALLBACK CANCELLED | 200 (OK) |
| 253 | INFO | CALLBACK ALREADY FAILED | 200 (OK) |
| 254 | INFO | CALLBACK SLOT BLOCKED OUT | 200 (OK) |
| 255 | INFO | CALLBACK STILL IN PROGRESS | 200 (OK) |
| 256 | INFO | CALLBACK EITHER NOT STARTED OR ALREADY COMPLETED | 200 (OK) |
| 257 | INFO | CALLBACK NOT LOCKED | 200 (OK) |
| 258 | INFO | CANNOT UNSUSPEND WHILE CALLBACK ONGOING | 200 (OK) |
| 259 | WARNING | ENVIRONMENT NOT ENABLED FOR USE WITH THIS CONSUMER AND/OR APPLICATION | 200 (OK) |
| 260 | INFO | UNDERGOING MAINTENANCE | 503 (Service Unavailable) |
| 261 | CRITICAL | WRITE DATABASE CONNECTION FAILED | 503 (Service Unavailable) |
| 262 | CRITICAL | READ DATABASE CONNECTION FAILED  | 503 (Service Unavailable) |
| 263 | CRITICAL | WRITE DATABASE CONNECTION TIMEEDOUT | 503 (Service Unavailable) |
| 264 | CRITICAL | READ DATABASE CONNECTION TIMEOUT | 503 (Service Unavailable) |
| 265 | WARNING | NO CUSTOMER FEEDBACK CONFIGURED | 200 (OK) |
| 266 | INFO | INVALID PAYMENTLINKREFERENCEID | 200 (OK) |
| 267 | INFO | EMPTY LOGIC EXPRESSION | 200 (OK) |
| 268 | INFO | EVALUATED LOGIC EXPRESSION FAILED | 200 (OK) |
| 269 | INFO | SESSION OUT OF SCOPE | 401 (Unauthorized) |
| 303 | INFO | NO AD DATA | 200 (OK) |
| 304 | INFO | NO AD DATA | 200 (OK) |
| 305 | INFO | NO KNOWLEDGE DATA | 200 (OK) |
| 306 | INFO | NO KNOWLEDGE DATA | 200 (OK) |
| 307 | INFO | NO KNOWLEDGE DATA | 200 (OK) |
| 309 | INFO | INVALID VIEW | 200 (OK) |
| 310 | INFO | DATA NOT MODIFIED | 304 (Not Modified) |
| 311 | INFO | INVALID DATE RANGE | 200 (OK) |
| 312 | INFO | MAGIC LINK EXPIRED OR INVALID | 200 (OK) |
| 313 | INFO | REACHED MAX DATA DOWNLOADS | 200 (OK) |
| 314 | INFO | STREAM LOG ERROR RETRYING | 200 (OK) |
| 403 | INFO | NOT AUTHORISED | 403 (Forbidden) |
