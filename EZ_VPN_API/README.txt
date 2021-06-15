[www.ezvpn.online](https://www.ezvpn.online/)

EZ VPN API allows you to deploy, provision, and manage VPN tunnels to your remote networks.
With our API, you do not need to act manually on the management site.

You can deploy and manage thousands of Boxes, Users, with your script or from your code or your applications.

# Beta #

Please note that EZ VPN API is still in Beta version. The current specifications are subject to change, with no advice.
When we migrate to the production status, all the API users will be informed accordingly.

# Description #

EZ VPN API is organized around REST and uses HTTP verbs and response codes that most clients are familiar with.

All requests must be formatted as `Content-Type: application/json` (except where noted).

All responses are also formatted JSON, encoded in the `UTF-8` character encoding (`Content-Type: application/json; charset=utf-8`).

The `Accept` header will be ignored for all requests.

# Security #

EZ VPN API uses the JWT flow for authentication and allows applications to submit authenticated requests on behalf of individual EZ VPN users enabled as developers.

1. First, invoke the `/login` endpoint using your developer key to get an authentication token and a userUUID token, from the JSON response body.

2. Once you’ve done that, you include your tokens with any of your EZ VPN requests.

An authorization header containing a valid access token and a UserUUID must be included in every EZ VPN API request as follows:

```
Authorization: Bearer YOUR_TOKEN
UserUUID: YOUR_UserUUID
```

e.g.

```
Authorization: Bearer xyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWYiOiJWVTJOMVdNVUpKQ0NRQ0X8VjJFRkFVUUlYRVBHWEhVTCIsImV4cCI6MTU2MjcxMDAzOH0.wDcjR7xyy8WFERY-zGbXDXobGdHHl-Ii8yb1rjb-oCq5aKhFB_jx2Nf73bYlpG1UieVhEXbrA5q6TXLYNSWikA
UserUUID:"YmZlOTc4MDkzYzA0ZrdmYmJhNmZjMWY1OTc3ODk5MTkwOTFiOThlYTBhMDllXmIxYTViYTU0NjRkNDEyOTBiOA=="
```

# HTTP Status Codes #

The following HTTP Status Codes are used by the API for correct replies.

| Status Code | Meaning                                                                                  |
| ----------- | ------------------------------------------------------------------------------------------------------ |
| 200         | Successful - Successful HTTP request.                                                                  |
| 201         | Created - The request has been fulfilled, resulting in the creation of a new resource.                 |
| 202         | Accepted - The request has been accepted for processing, but the processing has not been completed. |

If not documented, the returned  HTTP Status Code is 200.

# Errors #

When an error is encountered, you will receive an HTTP status code along with a message and error code in the body of the response. The message is intended to give a user-friendly explanation of the error while the error codes are designed to be machine-readable codes that applications can use to better understand the context of the error and react appropriately.

| Status Code | Meaning                                                                                  |
| ----------- | ---------------------------------------------------------------------------------------- |
| 400         | Bad Request – The request contains errors.                                               |
| 401         | Unauthorized – The authentication process failed, or the access token is not valid.      |
| 403         | Forbidden – Access to this resource is restricted for the given caller.                  |
| 404         | Not Found – The specified resource could not be found.                                   |
| 423         | Locked – the resource is not ready to be managed.                                        |
| 429         | Too Many Requests – API rate limit usage exceeded                                        |
| 500         | Internal Server Error – There was a problem with the API host server. Try again later.   |
| 503         | Service Unavailable – API is temporarily offline for maintenance. Try again later.       |

Error example response body:
```
{
    "timestamp": 1563402036854,
    "status": 404,
    "message": "Not Found",
    "details": "uri=/api/1.0/box/byUuid/0sdoNNNwVt0a7wI"
}
```

`timestamp` contains the number of milliseconds elapsed since Epoch (1/1/1970).

# Developer Keys #

In order to use the API, you need to enable the Developer features and obtain the API keys.

You can enable the developer API keys in the [management web site](https://management.ezvpn.online/).

Please note that the keys will be generated and shown just **once**, at generation time. It will not be possible for us to show you the keys again because saved as encrypted. If you ever lose the keys, you will have to regenerate new keys.

Store your keys safely, in a safe and encrypted vault. DO NOT SAVE your keys in code in remote version control repositories (like GitHub, Bitbucket, etc.). Whoever has your keys, will be able to get access to your remote networks.

If you need to save your keys in your code in your version control system, please consider using code encrypting technologies, like `git-crypt`.

# Rate Limits #

API access rate limits are applied at a per-developer basis in unit time. Access to the API using a key is limited to 60 requests per minute (subject to change). In addition, every API response is accompanied by the following set of headers to identify your available limits and the status of your consumption.

| Header                          | Description |
| ------------------------------- | ----------- |
| `X-RateLimit-Limit`             | The maximum number of requests that the consumer is permitted to make per minute. |
| `X-RateLimit-Remaining`         | The number of requests remaining in the current rate limit window. Present on requests passing the rate limit checks.                            |
| `X-RateLimit-RetryAfterSeconds` | The number of seconds you need to wait before the current rate limit window resets. Present on requests **not** passing the rate limit checks. |


# Monthly usage #

Access to the API using a key is limited to 2000 requests per month (per-account). Besides, every API response is accompanied by the following set of headers to identify your available limits and the status of your consumption.

| Header                     | Description |
| -------------------------- | ----------- |
| `X-MonthlyLimit-Limit`     | The maximum number of requests that the consumer is permitted to make per month (2000 by default). |
| `X-MonthlyLimit-Remaining` | The number of requests remaining in the current month. |

When `X-MonthlyLimit-Remaining` is 0, your monthly limit is over, and any further API call is not taken in charge.

The current month is computed and reset using UTC timezone.

If you need to increase the 2000/month calls limit, please contact EZ VPN support.

# API versions #

Base server url is `{{server-url}}`, used only by `/login` endpoint.

Each other API call must be prefixed using the correct base API url.

| version      | Full API Url                     |
| ------------ | -------------------------------- |
| Ver. 1.0     | {{server-url}}/1.0               |


# Conventions #

In the following sections of the documentation:

* **{{yourJWTToken}}** must be substituted by the real value of the Authorization token (`token` field) obtained through the `/login` endpoint
* **{{YourUserUUID}}** must be substituted by the real value of the user uuid (`userUUID` field) obtained through the `/login` endpoint
