Introduction
=======

The Mailgun API is built on HTTP. Our API is RESTful and it:

* Uses predictable, resource-oriented URLs.
* Uses built-in HTTP capabilities for passing parameters and authentication.
* Responds with standard HTTP response codes to indicate errors.
* Returns JSON.

Mailgun has published [Libraries](https://documentation.mailgun.com/en/latest/libraries.html#libraries) for various languages. You may use our libraries, or your favorite HTTP/REST library available for your programming language, to make HTTP calls to Mailgun. Visit our Libraries page to see HTTP REST libraries we recommend.

To give you an idea of how to use the API, we have annotated our documentation with code samples written in several popular programming languages. Use the language selector at the top to switch between them.

Our samples from [quickstart](https://documentation.mailgun.com/en/latest/quickstart.html), [User Manual](https://documentation.mailgun.com/en/latest/user_manual.html#user-manual), and [API Reference](https://documentation.mailgun.com/en/latest/api_reference.html#api-reference) provide examples that will function. You’re welcome to copy/paste and run the script to see the API in action.

## Base URL

All API URLs referenced in this documentation start with the following base part:
> https://api.mailgun.net/v3

Your Mailgun account may contain several email domains. To avoid passing the domain name as a query parameter, most API URLs must include the name of the domain you’re interested in:
> https://api.mailgun.net/v3/mydomain.com

## Authentication

When you sign up for an account, you are given an API key. You authenticate to the Mailgun API by providing your API key in the request. You can manage your API key in the “Security” tab under the Account section of the Control Panel.

Authentication to the API occurs via [HTTP Basic Auth](http://en.wikipedia.org/wiki/Basic_access_authentication). Use `api` as the user name and your API key is the password. Here is how you use basic HTTP auth with curl:
> curl --user 'api:key-3ax6xnjp29jd6fds4gc373sgvjxteol0'

Or you can try the following API call right from your browser:
> https://api:key-3ax6xnjp29jd6fds4gc373sgvjxteol0@api.mailgun.net/v3/samples.mailgun.org/log

**Warning:** Keep your API key secret!

## Date Format

Mailgun returns JSON for all API calls. JSON does not have a built-in date type, dates are passed as strings encoded according to [RFC 2822#page-14](https://tools.ietf.org/html/rfc2822.html#page-14). This format is native to JavaScript and is also supported by most programming languages out of the box:

> 'Thu, 13 Oct 2011 18:02:00 GMT'

## Errors

| Code               | Description                                               |
|--------------------|-----------------------------------------------------------|
| 200                | Everything worked as expected                             |
| 400                | Bad Request - Often missing a required parameter          |
| 401                | Unauthorized - No valid API key provided                  |
| 402                | Request Failed - Parameters were valid but request failed |
| 404                | Not Found - The requested item doesn’t exist              |
| 500, 502, 503, 504 | Server Errors - something is wrong on Mailgun’s end       |

## Webhooks

Mailgun can also POST data to your application when events (opens, clicks, bounces, etc.) occur or when you use Routes. You can read more about webhooks and [Routes](https://documentation.mailgun.com/en/latest/user_manual.html#um-routes) in the [User Manual](https://documentation.mailgun.com/en/latest/user_manual.html#user-manual).

## Mailgun Regions

Using a single account and billing plan, you can choose to provision new sending domains in the EU environment. Message data never leaves the region in which it is processed. Only a limited amount of account data is replicated globally, giving you a single account from which to manage domains in both the US and the EU. Here are the specifics on the type of data that is replicated globally versus what is region-bound.

| Global                                                                                                  | Region-Bound (US / EU)                                                                                                             |
|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Account Information, User Accounts, Billing Details (invoices/plan information), API Keys, Domain Names | Domain Metadata (e.g. SMTP credentials), Messages, Event Logs, Suppressions, Mailing Lists, Tags, Statistics, Routes, IP Addresses |

The endpoints you will use for sending/receiving/tracking messages in the EU are below:

| Service                      | US Endpoint      | EU Endpoint         |
|------------------------------|------------------|---------------------|
| REST API                     | api.mailgun.net  | api.eu.mailgun.net  |
| Outgoing SMTP Server         | smtp.mailgun.org | smtp.eu.mailgun.org |
| Inbound SMTP Server (Routes) | mxa.mailgun.org  | mxa.eu.mailgun.org  |
| Inbound SMTP Server (Routes) | mxb.mailgun.org  | mxb.eu.mailgun.org  |
| Open/Click Tracking Endpoint | mailgun.org      | eu.mailgun.org      |