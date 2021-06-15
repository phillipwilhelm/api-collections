Welcome to the Slyp Bank API!

This information is intended as a technical reference for developers at partner Banks. Included is a full specification of each of the Slyp API endpoints relevant to banking partners, including request examples with sample code in multiple languages, use cases and response formats.

For any assistance, error reporting or feedback please contact dev@slyp.com.au

# API

The following applies to the entire Slyp API, and is considered assumed knowledge throughout the rest of this resource.

The Slyp API is based on RESTful principles with predictable, resource-oriented URLs and uses HTTP response codes to indicate successful API calls and errors. The API has built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients.

Data Type definitions are included throughout this documentation to accompany request/response formats that use them. Required fields marked by an asterisk. Fields that are not required may be omitted in requests, and will typically be set to a default value of `null` unless otherwise stated. The fields included in a particular response instance may vary according to context, such as the role of the user making the request. For example, some attributes of a `Receipt` that are set by Consumers are not available to Merchants and vice versa.

JSON is returned by all API responses, including errors.


# Errors

Slyp makes use of standard HTTP response codes to indicate the outcome of an API request, as follows:
- `2XX` response codes indicate success,
- `3XX` response codes indicate a previous success,
- `4XX` response codes indicate a failure, with additional information provided to elaborate on the reason for the failure,
- `5XX` response codes indicate an error within the Smart Receipt solution.

| |HTTP CODE SUMMARY|
|---:|---|
|200 - OK|Everything worked as expected.|
|201 - Created|The resource was created successfully. Resulting from a successful `POST` request.|
|400 - Bad Request|The request was invalid - generally due to missing, required or invalid parameters.|
|401 - Unauthorized|The API key or JWT provided was invalid or not authorised for this resource or action.|
|402 - Request Failed|The parameters were valid but the request failed.|
|404 - Not Found|The requested resource doesn't exist.|
|409 - Conflict|The resource already exists. Generally resulting from using the same idempotent key.|
|429 - Too Many Requests|Too many requests hit the API too quickly. We recommend an exponential back-off of your requests.|
|500, 502, 503, 504 - Server Errors|Something went wrong on our end. (These are rare.)|

*Error Response Sample:*
```JSON
{
  "status": 401,
  "msg": "Unauthorized",
  "code": "", // Programatic error codes not yet implemented
  "request_id": "", // unimplemented correlation id for the request
  "detail": {} // arbitrary object for including further information or raw error responses
}
```

# Pagination

All top-level API resources have support for bulk fetches via "list" API methods. For instance you can list Receipts, list Promotions, and list Merchants. These list API methods share a common structure, taking two optional parameters: `limit` and `offset`.
<br/>

| |ARGUMENTS|
|---:|---|
|**limit**<br/>Integer<br/>Default: 10|A limit on the number of objects to be returned per page, between 1 and 100.|
|**offset**<br/>Integer<br/>Default: 0|The number of records to skip offset by.|

| |LIST RESPONSE FORMAT|
|---:|---|
|**current_offset**<br>Integer|The offset used for this query from 0 index (the first item is item 0).|
|**next_offset**<br>Integer|The offset the client should use when making the next query to get the next 'page'.|
|**items**<br/>Array|An array containing the actual response elements, paginated by any request parameters.|
|**total**<br/>Integer|The total number of records available for given request parameters.|

Example with offset to receive next page after the first 10 have already been received: 
> `.../merchants/:id/receipts?offset=10`
Example with offset and limit to retrieve only the second item:
> `.../merchants/:id?receipts?offset=1&limit=1`

# Sorting

API responses with lists of data can be sorted by providing a sort parameter in the query string such as `sort=total_price` on a receipts request.

The parameter may be prepended with a + or - to specify a sort order. The default is ascending (+). eg: `sort=-total_price` would sort items based on the `total_price` field in reverse order.

By default, if no sort parameters are specified, the sort order is ascending on the default sorting field (typically time based, such as time of creation). Pass `sort=desc` in the query string to reverse the order on the default sorting field.

# Versioning

When necessary backwards-incompatible changes to the API are released, we release a new versioned prefix. The current version is `/v1/`. Read our API upgrades guide to see our API changelog and to learn more about backwards compatibility.

> *As a precaution, use API versioning to test a new API version before committing to an upgrade.*