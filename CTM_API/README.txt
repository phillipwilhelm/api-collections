The CallTrackingMetrics API provides a RESTful interface to call data, phone numbers, text messaging, and account management. To assist in integrating CallTrackingMetrics with your website, we also provide a JavaScript API that allows you to customize how our dynamic number swapping interacts with your website.

You may make requests using any of the following content types in the request header:

* Content-Type: application/json
* Content-Type: application/x-www-form-urlencoded
* Content-Type: multipart/form-data

Make sure the body matches the Content-Type. For example if you are going to submit a JSON body like { "phone_number": "+18085551212" }, make sure to make the request with a Content-Type: application/json header as well.

All REST API endpoints respond with JSON encoded data.

* Content-Type: application/json

# Authentication

We support two levels of REST API access: single account level and multi account level.

Single Account Level access grants you access to a single account and can be enabled within the Account Settings page for each account.
Multi Account Level access grants you access to all sub-accounts within an agency or enterprise account and can be enabled within the Agency Settings page.
For either level, once you have enabled API access, you will have an Access Key and Secret Key. Once enabled, there are also buttons to reset the keys or disable API access.

To authorize with the API we use Basic Authentication.  You will use the API key and secret either for your account or agency to construct an Authorization header that is base64 encoded.  For example:

```
GET /api/v1/accounts.json HTTP/1.1
Host: api.calltrackingmetrics.com
Authorization: Basic Y3RtOnNlYw.....
```

# API Usage / Rate Limits

CTM has the following limits on API usage:
   1.  10 requests / second.
   2.  Excessive errors may be throttled

# API Reference