## Introduction
<br>

The [Quicko](https://quicko.com) API provides digital infrastructure you will need to quickly integrate and offer IT, [GST](https://quicko.com/gst/api), TDS & [PAN](https://quicko.com/pan/api) compliance in your products and workflows.

It's really easy to use Quicko APIs & start consuming them in your app. Using Quicko API, you can consume a unified, REST format that is easy to understand and embed in your app. Moreover, you can signup, subscribe & start consuming all of the APIs using the [dashboard](https://dashboard.api.quicko.com). Our APIs have simple, resource-oriented URLs, accepts JSON-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication and error messages. 

<br>
<br>

### Terms of Use

Thank you for using Quicko’s APIs, other developer services, and associated software (collectively, “APIs”). By accessing or using our APIs, you are agreeing to the terms as written [here](https://support.quicko.com/hc/en-us/articles/360040187212-Terms-of-Use).
<br>
<br>

### REST clients

REST clients such as Postman or Insomnia allow you to make requests to the Quicko REST APIs using a well-designed visual interface. The easiest way to start using the Quicko API is by clicking the Run in Postman button above. Postman is a free tool which helps developers run and debug API requests, and is the source of truth for this documentation. Every endpoint you see documented here is readily available by running our Postman collection.
<br>
<br>

### Version and API Endpoint 

The current (stable) version is 3.2. All requests will use this default setting, unless you override the API version. It is recommended that a specific version be requested explicity for production applications as major releases may break older implementations. To set the API version on a specific request, set the HTTP header `x-api-version` header with version number. Root endpoint for Quicko API is : https://api.quicko.com/.
<br>
<br>

#### Sandbox environment

The current (stable) version is 3.2. Root endpoint for Quicko Sandbox API is : https://sandbox.api.quicko.com.

You can generate credentials for Sandbox environment from API Dashboard. The Sandbox environment enables simulated business activity and lets developers build, test, and monitor applications integrated with Quicko. This Sandbox environment will provide mocked responses reflecting behavior in production environment.
<br>

Read [Sandbox API](#sandbox-api)


<br>
<br>

### Libraries and SDKs

You can use pre-built client to interact with Quicko API v3.2.1 without having to make raw HTTP calls.

* [Version 3.2.1](https://github.com/TeamQuicko/quicko-api-client/releases/tag/v3.2.1)
<br>
<br>

### API Status

Available at [Quicko API Status](https://quicko.freshstatus.io), Quicko API status reports uptime and incidents for our API environments.
<br>
<br>


### Need help?

Get help by mailing our support team at [developer@quicko.com](mailto:developer@quicko.com?subject=[Quicko%20API]) or Call us 7575831310.

<br>
<br>

<a href="https://dashboard.api.quicko.com" target="_blank">Sign up for API access</a>

<br>
<br>
<br>

---


# Response structure
<br>
All GET and DELETE request parameters goes either as path parameter or as query parameters, and POST parameters as (Content-Type : application/json) body, responses from the API are always JSON. The responses may be Gzipped.
<br>
<br>

### Successful request

All responses from the API server are JSON with the content-type application/json. A successful 200 OK response always has a JSON response body except for DELETE request. The response contains the full payload. Every API response contains entities that are shared across different endpoints. There are some common attributes for entity.
<br>
<br>


| Property	| Type			| Description						|
|---		|:-:			|---								|
| @entity	|`string`		| Indicates the type of entity		|
| id		|`hex(32)`  	| Unique identifier of entity		|



<br>
<br>
<h5>Example Object</h5>


    HTTP/1.1 200 OK
    Content-Type: application/json
    {
        "@entity": "object"
        "id": "51A565413C35B5565718756153019872"
    }
<br>

### Failed request

We use conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a charge failed, etc.), and codes in the 5xx range indicate an error with our servers. A failure response is preceded by the corresponding 40x or 50x HTTP header. The code key in the response envelope contains the REST status code. The message key contains a textual description of the error.
<br>




    HTTP/1.1 403 Forbidden
    Content-Type: application/json
    {
        "code": 403,
        "message": "Access denied"
    }
<br>

### Data types

Values in JSON responses are of types string, bigdecimal, date or boolean. All date are in DD/MM/YYYY format set under the Indian timezone (IST) (Local time as in Asia/Kolkata)


<br>
<br>
<br>

---


[//]: # (This is a comment. Don't modify header below. Might be used to interlink article)
## Common Entities
<br>

Common entities reused accross APIs such as address, contact, bank account, etc. are described below.
<br>
<br>

[//]: # (This is a comment. Don't modify header below. Might be used to interlink article)
### Address Entity
<br>
The various properties are explained below:

	
| Param					| Type				| Description														|
|---					| :-:				|---																|
| area					| `string`			| Area																|
| city					| `string`			| City																|
| country				| `string`			| Country															|
| district				| `string`			| District															|
| full_address			| `string`			| Full address														|
| id					| `hex(32)`			| Unique address identifier											|
| is_primary			| `boolean`			| Whether it is primary address or not								|
| postal_code			| `string`			| Postal code														|
| street				| `string`			| Street															|
| type					| `string`			| Type of address. Possible values: `Home`, `Work`, `Shipping` and `Billing` 									|

<br>
<br>

[//]: # (This is a comment. Don't modify header below. Might be used to interlink article)
### Contact Entity
<br>
The various properties are explained below:

	
| Param					| Type				| Description														|
|---					| :-:				|---																|
| email					| `string`			| Email																|
| id					| `hex(32)`			| Unique contact identifier											|
| mobile				| `string`			| Mobile number														|

<br>
<br>

[//]: # (This is a comment. Don't modify header below. Might be used to interlink article)
### Bank Account Entity
<br>
The various properties are explained below:

	
| Param					| Type				| Description														|
|---					| :-:				|---																|
| account_number		| `string`			| Account number													|
| bank_name				| `string`			| Bank name															|
| id					| `hex(32)`			| Unique bank account identifier											|
| ifsc					| `string`			| IFSC code															|
| is_primary			| `boolean`			| Whether it is primary bank account or not							|
| type					| `string`			| Type of bank account. Possible value: `Savings` and `Current`		|

<br>
<br>

[//]: # (This is a comment. Don't modify header below. Might be used to interlink article)
### Document Entity
<br>
The various properties are explained below:

	
| Param					| Type				| Description														|
|---					| :-:				|---																|
| document_creation_date| `date`		| Document creation date											|
| document_name			| `string`			| Document name														|
| id					| `hex(32)`			| Unique document identifier											|
| signed_url			| `string`			| Signed url to document											|
| type					| `string`			| Type of document. Possible values: `Form-16`, `Form 27Q`, `Form 26Q`, `Form 24Q`, `ITR`, `ITR-V`, `Signature`, `Aadhaar`, `Bank Statement`, `Birth Certificate`, `Certificate of Incorporation`, `Driving License`, `Voter Id Card`, `Electricity Bill`, `Marriage Certificate`, `PAN`, `Passport`, `Rent Agreement`, `Telephone Bill`, `Mobile Bill`, `Form-49A`, `Acknowledgement`, `Salary Slips`, `Profit and Loss Account`, `Balance Sheet`, `Demat Account Ledger`, `Contract Notes`, `Purchase Deed`, `Sale Deed`, `National Savings Certificate(NSC)`, `Fixed Deposit Certificate`, `Insurance Premium Receipt`, `Pension Fund Receipt`, `Tution Fees Receipt`, `Donation Receipt`, `Disability Certificate`, `Tax Deduction Certificate`, `Form-16A`, `Form-26AS`, `Tax Payment Counterfoil`, `Passbook`, `LLP Agreement`, `Gas Bill`, `Property Tax Bill`, `NOC`, `INC-9`, `INC-10`, `DIR-2`, `MOA Subscriber Sheet`, `AOA Subscriber Sheet`, `LLP Subscriber Sheet`, `Form-12BB`, `Rent Receipt`, `Computation of Income`, `Challan`, `TDS Return`, `FVU`, `Form-27`, `TDS Return Acknowledgement`, `TDS Return Statistics`, `Consolidated Statment`, `Income Tax Notice`, `Invoice`, `Purchase Order`, `Estimate`, `Bill of Supply`, `Debit Note`, `Credit Note`, `Logo` and `Other`							|

<br>
<br>

---

[//]: # (This is a comment. Don't modify header below. Might be used to interlink article)
## Common HTTP error codes
<br>

|Code	|Description																		|
|:-:	|---																				|
|400	|Missing or bad request parameters or values										|
|401	|Authorization failure																|
|403	|Authentication token expired/missing error											|
|404	|Requested resource was not found													|
|413	|Request is too large																|
|429	|Too many requests to the API (rate limiting), Quota exceeded error					|
|500	|Something unexpected went wrong like accessing invalid API, invalid endpoint, etc.	|
|504	|Gateway timeout; the API is unreachable											|


<br>
<br>
<br>