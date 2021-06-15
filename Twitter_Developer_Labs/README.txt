# Postman collection for Twitter Developer Labs
This is a Postman collection for the developer previews in [Twitter Developer Labs](https://developer.twitter.com/en/labs?utm_source=postman).

For more details, read the [Twitter Developer Labs documentation](https://developer.twitter.com/en/docs/labs?utm_source=postman).

**Remember:** The endpoints we release in Labs will be previews and are likely to change before they are released broadly, so we encourage you to take that into consideration as you build.

## Quick install

Just click the **Run in Postman** button. You're all set!

## Environment

This collection includes a environment variables that are needed to authenticate each request. You will need to add values to each variable.

|Name|Description|
|----|-----------|
|`consumer_key`|Your OAuth consumer key|	
|`consumer_secret`|Your OAuth consumer secret|
|`access_token`|Your OAuth access token|
|`token_secret`|Your OAuth access token secret|

To find these values:
1. Open your [app dashboard](https://developer.twitter.com/en/apps?utm_source=postman).
2. Select your app, then click **Details**.
3. Head over the **Keys and tokens** tab.
4. Copy the values into each variable.

To add these values to your Postman environment:
1. Select the ⚙️ icon next to the **Twitter Developer Labs** environment name.
2. Click **Twitter Developer Labs**.
3. For each variable, add the values from your app dashboard in the **Current value** column.
4. When you're done adding all values, click **Update**.

Postman will set up your requests to be authenticated using OAuth 2.0 (Bearer token) authentication.

## Get help

If you need help, ask a question in the [Labs community forums](https://twittercommunity.com/c/labs).

## Submit feedback

Your ideas matter! Help us develop the next generation of the Twitter API by [sharing your feedback](https://twitterdevfeedback.uservoice.com/).

We know the best future version of our API will come from creating it together with the people who use it most.