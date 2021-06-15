Build the best experience of digital signature through your own platform. Increase your conversion rates, leverage your data and reduce your costs with Yousign API.

Create your [free sandbox account](https://yousign.com/developer) to start the API integration.

## Welcome on Yousign for Developers!

Yousign provides an [API](https://en.wikipedia.org/wiki/Application_programming_interface) that allows you to optimize and automate your signature process directly through your own application. Please find below the full documentation which explains how to integrate our API step by step with concrete examples, use cases as well as source code.

By using this service, you will enjoy all features of Yousign's application and even more.

## API pricing

Click [here](https://yousign.com/prix/#api) for information on our API pricing.
On production environment, each API plan includes 1 user account for our Yousign application.

## We are here to support you!

Our priority is to ensure that you never feel abandoned. If you have any [technical](mailto:support@yousign.com) or [commercial](mailto:hello@yousign.com) questions or suggestions, feel free to contact us by email.

# Environments

In order to offer the most flexible integration, we provide developers with a completely free and unlimited test environment (our sandbox is named *Staging*).

To approach and take control of our API, developers will be able to build POC (Proof Of Concept) up to the end to end qualification stage without any constraint. This means that it's not necessary to contract and start paying to carry out the full development stage.


| **Environment** | **API Base URL**                    | **Web App URL**                     |
| --------------- | ----------------------------------- | ----------------------------------- |
| **Staging**     | https://staging-api.yousign.com     | https://staging-app.yousign.com     |
| **Production**  | https://api.yousign.com             | https://webapp.yousign.com          |

Notes: All **signed documents on staging environment are NOT legally signed**. The certificate used as part of these signatures will NOT comply with legal expectations and NO .txt proof file will be generated for your tests.

It is important to underline that both environments are completely independent and there is no link between them. This means that you will have one login / password and API keys for staging environment and another login / password and API keys for production environment. There is no native way to switch from test to live environment. Just use the appropriate API key and appropriate URL to perform a test or live procedure.

For more details on the transition to production, you should refer to the following section: Go live.

# Libraries

Currently, we don’t provide libraries or packages for specific programming languages. However, our API and webhooks use JSON. This format is widespread in the web ecosystem and you can easily find a parser for your favorite language.

Feel free to contact us if you built an open-source library for our API and want to share it with our developer community! Of course, Yousign will not maintain the provided libraries, but our team will be happy to simplify your integration even further.

Here is the list of libraries provided by the community:
- Language: GO > Go to the [Github repository](https://github.com/tbruyelle/yousign)
- Language: PHP > Go to the [Github repository](https://github.com/OlivierWizi/WiziYousignClient)
- Language: C# > Download the [package](https://s3.eu-west-3.amazonaws.com/ys-storage-public-content-bucket/api/code/20181217-laurenth-c-sharp.zip)

Many thanks to [Thomas Bruyelle](https://github.com/tbruyelle), [Olivier](https://github.com/OlivierWizi) and Laurent H.!

# Getting started

The Yousign API is a [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)ful interface, providing access to a wide range of the data in the system and especially to create signature procedures.

The API accepts [JSON](http://json.org/) content in requests and returns JSON content in all of its responses. This format is also forced by the Header `Content-Type`.

The [HTTP method](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) (like GET, POST, PUT, DELETE) determines the operation type on the resource (users, files, …). The resource is identified by the URL which is targeted by the method.

Example: `GET https://staging-api.yousign.com/users` will list all the details of users related to your organization.

To learn more about how the API works, you can consult the following links to understand how [HTTP status](https://dev.yousign.com/#244d14b0-a683-4930-b536-dbf87189735c), [pagination](https://dev.yousign.com/#06f20fd6-5fe0-4213-9edf-9ada6318e396), [filters](https://dev.yousign.com/#09638d14-159c-4425-ae00-b5f60e42ad04) and [data formats](https://dev.yousign.com/#a5db5290-0765-425f-b1fb-6901646e265c) work.

In addition, each identifier used to target a resource in our API is formatted from the following standard: [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random)) (UUID v4). This format is systematically composed as follows:
`XXXXXXXXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXXXX`. Finally, given the number of characters and therefore the number of possibilities, this random identifier format is secured and unpredictable.

Before implementing it in your platform, you can use software ([POSTMAN](https://www.getpostman.com/) for example) to send JSON requests and receive responses without writing any line of source code. It could be very helpful at the beginning to understand what will be the request format and simulate the workflow on your side with inputs / outputs.

To further facilitate the development of your Yousign API integration, we provide you a [Swagger](https://dev.yousign.com/?version=latest#d9bda911-06e9-4515-b7e6-d9f8a6d15cc2) through [Swagger-UI](https://swagger.yousign.com/) and [swagger.json](https://swagger.yousign.com/swagger.json).

Now let's see how to create your API key to start sending your first request!

## Step 1 - Create your account

First of all, you have to create your own free and unlimited account to access our application on our staging environment (sandbox). Let's start by clicking on one of the following links:

- [Sandbox Signup](https://yousign.com/developer)

After having entered your email address, you will receive a confirmation email allowing you to validate your account.

Notes: It is mentioned “*Free 14-day trial. No credit card required.*” on the signup page but there is no limit in time to use this service on the test environment.

On this environment, you will be able to create up to 10 users on your organization. Therefore, if you are a team of developers working on this wonderful project, you will all have access to the same information including sharing the API keys.

It's important to underline that on the production environment, each user account will be billed according to the selected plan (except the first user that will be included in your API plan).

## Step 2 - Create your API key

Once you have access to our application, then you have to create an API key to access our routes (menu: Admin > API keys > Create).

1. Logon on Yousign app: https://staging-app.yousign.com
2. Create your first API key here: https://staging-app.yousign.com/admin/apikeys

Your API keys carry many privileges, so be sure to keep them secure! With these tokens, anyone can access to all information stored for your organization (users, files, ...). Do not share your secret API keys in publicly accessible areas.

On our application, only users with administrator privileges will access to API keys.

If you don't see any access to Admin menu or API key tabs, please contact your organization administrator or our [technical support](mailto:support@yousign.com).

## Step 3 - Authentication

Once your API key generated, you will be able to send and receive HTTP requests from our server.

Access to the API is performed via **Bearer Authentication** that involves security tokens called bearer tokens (so this is the API key).

Your request has to include `Authorization` header with your API key to be authenticated:

 `Authorization: Bearer [YOUR_API_KEY_HERE]`

For security reasons, you can only use our API through [HTTPS](https://en.wikipedia.org/wiki/HTTPS) protocol. Calls made over plain HTTP will fail. You have to authenticate for all requests with Bearer authentication.

Notes: The API keys are different for your test site and your live site.
