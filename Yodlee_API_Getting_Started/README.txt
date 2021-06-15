[register]: https://developer.yodlee.com/user/register
[dashboard]: https://developer.yodlee.com/api-dashboard

Getting Started helps you quickly get an understanding of the Yodlee API.

For a fuller step-by-step tutorial introduction to Yodlee APIs and FastLink, see the [Quickstart Guide](https://developer.yodlee.com/vqs).
  
Before we begin, some keywords that you should know:  
  
**user:** End user of your application.  
**FastLink:** A Yodlee hosted widget that can be embedded into your website/app and allows users to search and connect their financial institutions.  

# Prerequisites
To complete this guide, you'll need to
* [Register][register] for a developer account.  
* Get your credentials from your [API dashboard][dashboard].  
* Pick one of the 5 [pre-registered test users](https://developer.yodlee.com/new-oauth-dashboard#testAccounts) to work with.

# Using the API calls
All calls require these [Postman variables](https://learning.postman.com/docs/sending-requests/variables/) to be set:
  
**host** The url for your environment. For a Sandbox account, this would be https://sandbox.api.yodlee.com/ysl/  

**userName** - For Sandbox you can copy/paste one of the test users from your [dashboard][dashboard].

**clientId** - Copy/paste your `clientId` from your [dashboard][dashboard].

**secret** - Copy/paste your `secret` from your [dashboard][dashboard].

# Generating a Token
This guide has a step for generating an authorization token.
Be sure to run that call before any of the others.

To generate an auth token in your app, please follow the steps described [here](https://developer.yodlee.com/docs/api/1.1/getting-started-with-cc)

# Linking a Bank Account
Yodlee provides the FastLink tool for linking accounts.
Learn about FastLink 4.0 [here](https://developer.yodlee.com/docs/fastlink/4.0/landing)

To link an account to work with this guide, you may run FastLink via [Codepen](https://codepen.io/team/yodlee-dev-ex/pen/zYrQrzJ?editors=0010).
You will need to create and copy over an auth token, and set the FastLink URL.

<b>Using dummy data</b>
The Yodlee Sandbox allows you to access realistic dummy account data.

To link a dummy account, run FastLink.
Choose "Dag Site" for the provider.
Use "YodTest.site16441.2" for the username and "site16441.2" for the password.

# Endpoints