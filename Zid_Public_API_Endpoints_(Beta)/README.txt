# Overview
Zid API allows you to use some of the most important functionalities of Zid platform to perform jobs in your app using our merchants' store data.

# Prerequisites
1. A background on any programming language that supports RESTful API either natively or through a library.
2. Experience with RESTful API.
3. A background on Zid system especially merchant dashboard specifications.
4. A background on webhooks (to receive Zid event notifications).
5. Access to a store on Business or on Growth plan to be able to get the manager token.

# How to integrate with Zid?
1. Make sure to read and to understand Zid API documentation.
2. Fill [this form](https://zid-services.typeform.com/to/TlK5sckY) to create a developer account for you and to generate your app authorization token and to provide you with environment variables.

# Considerations
1. In our internal applications, we use the same API endpoints we provide to external developers, that's why we keep them high maintained, since if they are broken, then our internal applications are broken as well.
2. Don't rely on the auto-generated examples by Postman, you have to understand how to call RESTful API endpoints from the programming language you're writing your application with.
3. Please pay attention to Authentication instructions since you'll need 2 different tokens to authorize your application.
4. Keep an eye on https://status.zid.sa

# FAQ

**- Where is your testing environment?**

We only provide production environment so you'll have to test the API against a real store, we will be working on providing a solution to avoid that.

**- What's the difference between Authorization token and X-MANAGER-TOKEN?**

    1. Authorization token permits you to access Zid API
    2. X-MANAGER-TOKEN permits you to access a particular store.

**- What's the difference between X-MANAGER-TOKEN and Access-Token?**

There is no difference between those two, but we use Access-Token with Product component API endpoints for technical reasons.

---

# Authentication
Zid API uses Bearer Authentication, to obtain your key, please fill [this form](https://zid-services.typeform.com/to/TlK5sckY).
Once you have your key, you can set in the "Authorization" header as follows:
```
Authorization: Bearer <YOUR_TOKEN>
```

To authorize your app against a certain store, you have to set the X-MANAGER-TOKEN / Access-Token header. As a merchant, you can get this token from https://web.zid.sa/account/settings/integrations/zid.


**NOTE: The store you're testing against should be either on Growth or Business plan, otherwise you wouldn't be able to generate the token.**

```
X-MANAGER-TOKEN: <STORE_MANAGER_TOKEN>
```
*Please consider that the manager token expires in 6 months.*

You will also need the store id for some endpoints.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

# Documentation Version
Version: 0.2.0 Beta

Publish Date: 2020-01-15

# Base URL and versioning
API production base URL: **api.zid.sa**.

API version is specified at the end of the after the base URL. e.g., api.zid.sa/v1/

The latest version is **v1** older versions are **deprecated** and should not be used.

# User-Agent
User-Agent is a required header in most of our API endpoints, make sure to set it to your application or company name with this format **App-Name/1.00.00 (web)**.

Where **1.00.00** is your app version, you can change the digits as you wish.

The user agent will be used to prevent infinite webhook requests, which makes it very important if you intend to use the [webhooks](https://docs.zid.sa/?version=latest#54e87abb-3a57-498f-bd75-e01603493aff).

# Error Codes
**TODO**

# Rate limit

Zid implements the [Leaky Bucket](https://en.wikipedia.org/wiki/Leaky_bucket) algorithm for rate limiting, which means requests will be served and when you hit the bucket limit requests may be throttled or dropped.

# Changelog
All notable changes to this API will be documented in this section.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),