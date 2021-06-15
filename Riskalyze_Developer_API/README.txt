Welcome to the Riskalyze API website! Here you will find detailed information about the various endpoints for the Riskalyze API. The Riskalyze API utilizes OAuth 2.0 with the authorization code flow. For more on OAuth 2.0 with authorization code, see https://oauth.net/2/grant-types/authorization-code/

# Security Policy
We take breaches of security very seriously at Riskalyze. If you have had a security breach in which any Riskalyze data or credentials may have been compromised, contact us immediately at <a href="mailto:api@riskalyze.com">api@riskalyze.com</a>.

While the following is not meant to be an exhaustive list, below are some examples of what would constitute a security incident that could cause the temporary suspension or permanent termination of your API access.

1. Use of a non-test Riskalyze account with your test API credentials

2. Launching your solution to production without first passing Riskalyze’s review

3. Launching your solution to production with your test API credentials

4. Insecurely handling or transmitting your OAuth client secret. There is NEVER a reason to send us your OAuth client secret outside of our API.

5. Insecurely handling or transmitting an OAuth auth code, access token, or refresh token. There is NEVER a reason to send us an auth code, access token, or refresh token outside of our API.

6. Insecurely implementing the Riskalyze API

7. Allowing one user to see another user’s data

8. Obtaining, storing, transmitting, or using the username and password of one of our customers

Please consult your API agreement for further provisions.

# API Access
Access to the Riskalyze Developer API is by approval only. In order to do this, contact your account representative.

Every request that your application sends to a Riskalyze API needs to be identified. Once you have obtained API credentials, you can connect to our API with an OAuth 2.0 access token in your request.

# API Calls
Riskalyze APIs utilize a RESTful design. This means that you use standard HTTP methods to retrieve and manipulate objects. The base url for Riskalyze APIs is https://api2.riskalyze.com/.

*Note:* All requests to the API must be made via HTTPS protocol and include proper API credentials. 

*For Local Development in Postman:* If you want to begin using this collection locally on your postman instance click the "Run In Postman" tab to download this collection to your local postman instance. You can mock the riskalyze production requests and responses by using the "mock server" feature provided by postman.  You will need to change the base url from https://api2.riskalyze.com/ to the postman mock base url, https://d739a0eb-c045-4be3-a599-8d64826ba1bc.mock.pstmn.io/

## Request Methods
The Riskalyze APIs expose various endpoints for working with resources. Each endpoint supports one or more of the following HTTP request methods:

GET:	Used to retrieve an individual resource, a list of resources, or to search resources.<br/>
POST:	Used to create a new resource.<br/>
PUT:	Used to update a resource.<br/>
DELETE:	Used to remove a resource.

## Response Codes
The table below describes the most common response codes that you will receive from a request. In addition to the status code, most responses will receive a body with a JSON structure that represents the results of a successful request or additional error information.

200:	OK<br/>
201:	Created - Resource was received and stored successfully<br/>
202:	Accepted - Resource was received and stored for process at a later time<br/>
204:	Resource was deleted successfully<br/>
400:	Bad Request - Response body will contain more information<br/>
401:	Unauthorized - Response will include the WWW-Authenticate header<br/>
403:	Forbidden - The requested resource is not assigned to your API key<br/>
404:	Not Found - The requested resource does not exist at this time<br/>
500:	Internal Server Error - Something went wrong… try again later

# Quota
Calls to the API must made made in accordance with your API agreement. Please contact your account representative for additional details.

# Data Formats
At this time, all resources in the Riskalyze APIs are represented using JSON data formats. The details of each resource are documented in the appropriate API. Sometimes the actual resource returned by the API will vary slightly from the representation in that it may include additional properties. If any undocumented data is useful feel free to use it with the understanding that it could disappear at any time. If undocumented properties drive a compelling use case for your application, feel free to let us know and we will consider adding it to the API spec.

# Displaying Risk Numbers #
We offer two methods of displaying Risk Numbers: 

**Download** our <a href="https://www.riskalyze.com/style">art kit</a>

**Generate** Risk Number images via CDN. Generating Risk Number images via our CDN is the **preferred method**. To generate a Risk Number image via our CDN you will need to use an img tag with a URL of the following format: `https://1dc018be4716da4aaa18-5d73971c6ce0cd6d739efc4134c4b48a.ssl.cf2.rackcdn.com/v2/[TYPE]/[SIZE]/r[RISK NUMBER].[file extension (png or svg)]`

We offer the following types:

|Type | Description | Example |
|---|---|---|
|standard | Risk Number with no special formatting. This would be used for a Client Risk Number | ![alt text](https://1dc018be4716da4aaa18-5d73971c6ce0cd6d739efc4134c4b48a.ssl.cf2.rackcdn.com/v2/standard/60/r59.png "Standard Risk Number") |
|portfolio | Risk Number formatted for displaying a portfolio Risk Number | ![alt text](https://1dc018be4716da4aaa18-5d73971c6ce0cd6d739efc4134c4b48a.ssl.cf2.rackcdn.com/v2/portfolio/60/r59.png "Portfolio Risk Number") |

We offer the following sizes, in pixels: 60, 90, 180, 360, and 1000. We also offer the graphics in the svg format. To get an svg, use svg for the size.

Risk Numbers can be 1 through 99. Sending a Risk Number of 0 will return a faded question mark for an unknown Risk Number

Example (png): https://1dc018be4716da4aaa18-5d73971c6ce0cd6d739efc4134c4b48a.ssl.cf2.rackcdn.com/v2/standard/360/r59.png

Example (svg): https://1dc018be4716da4aaa18-5d73971c6ce0cd6d739efc4134c4b48a.ssl.cf2.rackcdn.com/v2/standard/svg/r59.svg