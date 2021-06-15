The Open Banking Nigeria API specifications allow Nigerian financial institutions, FIs, (e.g., banks, mobile money operators, ATM providers) to develop API endpoints that can then be accessed by API users (e.g., third-party developers, fintechs) to build mobile and web applications for their customers.

These specifications allow FIs to provide a standardized interface that will enable fintechs and other stakeholders to access their products and services. For example, let customers to see all their accounts across multiple banks or to give instructions such that their accounts can be debited to pay for equities being bought on their behalf by their stock brokers.

The Open Banking Nigeria API is currently under development. Suggestions and comments are welcomed. To contribute or know more, kindly email contact@openbanking.ng. 

---

# What Open Banking will Achieve
Open Banking Nigeria allows account holders to seamlessly and securely link their bank account information with their platform or apps of choice.

Through the Open Banking API, a fintech can quickly create secure and personalized products and apps for its customers. While you can get access to our sandbox to start testing Open Banking in minutes, you would need to connect with real banks to be able to do real-life transactions.

All data presented here are dummy values.

To know more about Open Banking Nigeria and its advocacy to get Nigerian banks to adopt the same API standard, please visit the [Open Banking Nigeria website](https://openbanking.ng).

---

# Environments
We will provide multiple sandboxes that allow you to explore, develop and integrate with your applications, before progressing to test against your partner banks. Kindly note the following specifications:

| Environment      | What's it for? | 
| :---        |    :----:   |
| Postman      | Request a token to explore our API, make requests and receive responses with the Postman mock server       |
| Sandbox   | Request a token to explore the API set, make and receive data from a dummy banking setup        |

---

# Authentication
Authentication to the Open Banking API is performed via Bearer Authentication. Every endpoint requires authentication, so you will need to add the following header to each request:

`Authorization: Bearer <APIKey>`

---

# Implementation Phases
The standard we are developing can get complicated pretty quickly. Therefore, we have taken the liberty to phase the implementation across two phases. 

The first phase of version 1 (v1) covers meta, branches, ATMs, customers, accounts, and the ability to send money between accounts.

The second phase focuses on the complete transaction universe that a bank may want to implement.

---

# Data Types
All of the Open Banking Nigeria API responses returned are in JSON format, with these data types defined below:

|Type    | Description|
| ----------- | ----------- |
|string    | A UTF-8 encoded string|
|number    | An integer|
|datetime    | An ISO8601 encoded DateTime. All datetimes are returned in UTC with offset +00:00 |
|decimal    | All monetary values are returned with up to two decimal places and may be positive (20.78) or negative (-32.50) |


# Data Length

|Type    | Description|Length
| ----------- | ----------- | ----------- |
|Text fields    |string| max-length 255 characters
|BVN    |integers starting with 1 or 2 |11 digits.
|Account Number    | integers | 10 digits.


---

# Paging
For endpoints that provide several records, the response may be paged depending on the total number of records that the server can return at a time. This means that to retrieve the full set of items for a given resource you may be required to make several requests.

## URL Parameters
| Parameters | Description |
|-------------|-------------|    
|page|    The page number you wish to retrieve|
|limit|The number of items to return in a page|
|signature|Used to guarantee consistency of the data being returned|

## Response
| Field    | Type | Description
|-------------|-------------|-------------|    
|data|array|The actual data items you have requested|
|_meta|object|Key/value information that is not essential to understanding the resources returned but offers additional detail|
|_links|array|A collection of links that you can use to navigate the paged data|

## _meta
| Field    | Type | Description
|-------------|-------------|-------------|    
|totalNumberOfRecords |number |The total number of data items in the collection |
|totalNumberOfPages |number |The number of pages in the collection |
|pageNumber |number | The current page number|
| pageSize|number |The current page size |

## _links
| Field    | Type | Description
|-------------|-------------|-------------|    
|rel|string|The relation of the linked resource to the current resource |
|href|string|The absolute URI of the related resource |

## Navigating through pages
* If you are on the first page, the "prev" link will not be present in the response.
* If you are at the final page, the "next" link will not be present in the response
* If there are no pages and all data is returned neither "prev" or "next" links will be present in the response

---

# Errors
Errors in the Open Banking Nigeria API are expressed as a combination of HTTP status codes and an accompanying JSON body providing required detail where possible. You should be able to rely on the HTTP status code alone to determine the cause of the problem.

## Error Response Fields

| Field    | Type |
|-------------|-------------|    
| message    | `string`    A human-readable message as to the specifics of the problem. For example, it may contain a detail description of what caused the problem |
| status number | The HTTP status code used in the response |
| errorCode    number    | The specific Open Banking Nigeria error code for the problem

---

# Expansion Fields
The Open Banking API standard has been designed to be flexible enough to allow banks and other financial institutions to layer on additional data fields. This would help to pass on proprietary information not common to all banks or additional processing directives unique to the specific bank.

The `expansionFields` are optional and are a collection which means multiple instances of these fields may be included in any message.

## Response Body Fields
| Field |Type |Description |
| ----------- | ----------- | ----------- |
|id| string | A unique identifier for the extra field |
|description| string | A description of the extra field |
|type| string | A type of field but defined by the bank |
|value| string | The value of the extra field |

For this documentation, the `expansionFields` will not be included in the Response Body Fields

---
# Response Code
Find in the table below the possible response codes usually formatted as `status` and their respective descriptions. They follow the `8583 standards`.

| Code | Description |
| ----------- | ----------- |
| 00 | Approved or completed successfully |
| 01 | Status unknown, please wait for settlement report |
| 03 | Invalid Sender |
| 05 | Do not honor |
| 06 | Dormant Account |
| 07 | Invalid Account |
| 08 | Account Name Mismatch |
| 09 | Request processing in progress |
| 12 | Invalid transaction |
| 13 | Invalid Amount |
| 14 | Invalid Batch Number |
| 15 | Invalid Session or Record ID |
| 16 | Unknown Bank Code |
| 17 | Invalid Channel |
| 18 | Wrong Method Call |
| 21 | No action is taken |
| 25 | Unable to locate record |
| 26 | Duplicate record |
| 30 | Format error |
| 34 | Suspected fraud |
| 35 | Contact sending bank |
| 51 | No sufficient funds |
| 57 | Transaction not permitted to sender |
| 58 | Transaction not permitted on channel |
| 61 | Transfer limit Exceeded |
| 63 | Security violation |
| 65 | Exceeds withdrawal frequency |
| 68 | Response received too late |
| 69 | Unsuccessful Account/Amount block |
| 70 | Unsuccessful Account/Amount unblock |
| 71 | Empty Mandate Reference Number |
| 91 | Beneficiary Bank not available |
| 92 | Routing error |
| 94 | Duplicate transaction |
| 96 | System malfunction |
| 97 | Timeout waiting for a response from destination |

---
# Idempotency
Open Banking Nigeria API supports idempotency for safely retrying `POST` transactions without accidentally performing the same operation twice. This is useful when an API call is disrupted, and you do not receive a response. For example, `request_time_out` or `response_received_too_late`. Therefore, if you do not get a response message for a transaction, you can retry the request with the same idempotency key, and you are guaranteed that no more than one transaction would be posted.

To perform an idempotent request, provide an additional Idempotency-Key: <key> header to the request.

Open Banking Nigeria idempotency works by saving the resulting status code and body of the first request made for any given idempotency key, regardless of whether it succeeded or failed. Subsequent requests with the same key should return the same result, including Server (`500`) errors.

An idempotency key is a unique value generated by the Service Provide which the server uses to recognize subsequent transaction retries of the same request. It is up to the Service Provider to determine how these idempotency keys would be generated. Whatever it is, it must have enough entropy to avoid collisions.

Idempotency keys would never expire, so a new request that is generated if a key is reused outside of that time frame would fail.

Results are only saved if an API endpoint started executing. If incoming parameters failed validation, or the request conflicted with another that was executing concurrently, no idempotent result is saved because no API endpoint began execution. It is safe to retry these requests.

All `POST` requests accept idempotency keys and all transaction API calls must have idempotency keys. Sending idempotency keys in `GET` and `DELETE` requests has no effect and should be avoided, as these requests are idempotent by definition.