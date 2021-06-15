This Quickstart Guide will show the basics of verifying accounts using Yodlee.

[Account verification](https://www.yodlee.com/account-verification) can help enable payments, avoid overdrafts, reduce fraud, and more.

Verifying an account simply means getting detail information needed for the problem you're trying to solve.
For instance, for payments you might want to prove a user has access to an account, get the account routing number, and check the amount of money in it.

In this guide, we'll walk through all the steps needed to achieve complete flows for verifying account ownership, and checking balance information.
We'll also provide some other steps you can try out to dig deeper into the Yodlee API.

# How to Use This Guide

## Background

There's a few things you should know before beginning.
This guide assumes you'll be working in the [Yodlee Sandbox environment](https://developer.yodlee.com/docs/yodlee-environments-cc).

The Sandbox environment is available free once you [register][register] for a developer account.

Sandbox comes enabled with 5 preconfigured users.
It does not allow you to register new users.
It is also restricted to using dummy data, for security reasons.
Once you're comfortable and want to work without these restrictions, we recommend moving to the free [Launch Tier](https://developer.yodlee.com/pricing).

## Key Terms

**Users** - End users of your application.  In other words, your customers.  
**Providers** - Data providers.  The financial institutions, like banks, credit card companies, and so on.  
**Provider accounts** - This refers to the accounts your users use to access their provider information.  For example, if a bank has a web portal, your user has to login to an account to use it.  
**Accounts** - This refers to your users' accounts held by a provider, like a checking or savings account.  
**FastLink** - You need to connect or "link" your users to the accounts they hold. 
 FastLink is an embeddable Yodlee tool designed to make this easy.

A quick word about accounts.  Typically you'll be working with three different kinds:
*  **Provider accounts**.  These are the accounts your user, and, through Yodlee, you use to access banking, investment, and other financial services provider information.
* **Financial accounts**.  These are the traditional accounts like checking, savings, credit card, loan accounts, and so on.
* **Application accounts**.  These are the accounts you create to track and provide services to your customers.

## Prerequisites

To complete this guide, you'll need to
* [Register][register] for a developer account.  
* Get your credentials from your [API dashboard][dashboard].  
* Pick one of the 5 [pre-registered test users](https://developer.yodlee.com/new-oauth-dashboard#testAccounts) to work with.

## Postman

Most likely you've arrived at the [web version](https://av.developer.yodlee.com) of this guide first.
We created it using [Postman](https://www.postman.com/), a powerful tool for working with APIs, in the form of a [Postman Collection](https://www.postman.com/collection/).

You can load this collection into the Postman stand-alone tool and follow along making real API calls.
[Download](https://www.postman.com/downloads/)/open Postman first.  Then, look for the "Run in Postman" button at the top of this page.  Clicking that should allow you to load the collection directly.

From here on we'll assume you're working in Postman itself.

Postman lets you save entries you need for API calls for easy reference.  This is done with a [Postman Environment](https://learning.postman.com/docs/postman/variables-and-environments/managing-environments/).

Postman can automatically substitute in parameters for API calls from values kept in a Postman environment.  This collection comes with an environment preconfigured with several entries.  Working with the examples will be easiest if you fill in the appropriate values for these entries first.  Click on the eye icon next to the gear at top right of the Postman app window to open the editor and enter the values.

* **userName** - For Sandbox you can copy/paste one of the test users from your [dashboard][dashboard]. <br />
* **clientId** - Copy/paste your `clientId` from your [dashboard][dashboard]. <br />
* **secret** - Copy/paste your `secret` from your [dashboard][dashboard]. <br />

**&#x2757; Note: The Postman environment API URLs are set by default to the correct values for the United States.  If you're a customer in another region, be sure to copy/paste the appropriate URLs from your [dashboard][dashboard] into your environment.**

See the [Postman website](https://www.postman.com/) or the [Postman card](https://developer.yodlee.com/tools#CodingTools) on the Yodlee developer portal for more details.  Click on the image below for a quick visual tour of Postman.

><figure>
  <a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/t-1653/PostmanTour.mp4">
    <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/t-1653/PostmanTour.gif" alt="Navigating Postman">
    <figcaption>Click image to enlarge</figcaption>
  </a>
</figure>

Pay attention to the Test Results tab as you use this collection.  There are many guards in place to catch common mistakes.

[register]: https://developer.yodlee.com/user/register
[dashboard]: https://developer.yodlee.com/api-dashboard

# Diving in

Most applications verify an account only once.  Conversely, balance checks most often happen spread out over time.  Hence, the first flow includes linking an account.  The second assumes an account has already been linked.

With that in mind, we recommend walking through the two flows in order.  You can use accounts linked in the first flow to test the second, although normally there'd be a bigger gap between linking and refreshing.