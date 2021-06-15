<div align="center">
<img src="https://i.imgur.com/Dc0Cqe1.png" />
</div>

The Crypto Tracker is a Postman collection that leverages Airtable and CoinGecko to track a list of coins against specified thresholds and sends updates via SMS when coins go outside of the specified range.


Go from this
![](https://media.giphy.com/media/xTiN0DvoDyWQey2B8I/giphy.gif)

To this
![](https://media.giphy.com/media/AiULidifE382HGxt5U/giphy.gif)

**Hey, Listen!** To get the best value out of this collection you should run it as a [monitor](https://learning.postman.com/docs/designing-and-developing-your-api/monitoring-your-api/intro-monitors/) or with [Newman](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman) on a cron job so it runs on a periodic base.

![](https://media.giphy.com/media/I5DWjwUKUFlyXZ2haC/giphy.gif)
**Legal Disclaimer** The collection creator and Postman are not liable for any outcomes or decisions you make based on this collection. Use at your own discretion.

# Getting Started

[Create a new environment](https://learning.postman.com/docs/sending-requests/managing-environments/) or update the `Crypto Tracker.template` environment you downloaded with the **Run in Postman** button with the following variables.

## Twilio Variables

You will need a [Twilio Account SID](https://www.twilio.com/console/project/settings) (`twilioAccountSID`), [Twilio Auth Token](https://www.twilio.com/console/project/settings) (`twilioAuthToken`), [Twilio Trial Number](https://console.twilio.com/) (`twilioFromNumber`) and a [Twilio Verified Number](https://www.twilio.com/console/phone-numbers/verified) (`twilioToNumber`) to send SMS. These values need to be added to your current Postman Environment.

| Environment variable name | Description |
| - | - |
| `twilioAccountSID` | A [Twilio Account SID](https://www.twilio.com/console/project/settings) |
| `twilioAuthToken` | A [Twilio Auth Token](https://www.twilio.com/console/project/settings) |
| `twilioFromNumber` | A [Twilio Trial Number](https://www.twilio.com/console/) or a [Test Number](https://www.twilio.com/docs/iam/test-credentials#test-sms-messages) |
| `twilioToNumber` | Your [Twilio Verified Number](https://www.twilio.com/console/phone-numbers/verified) or a [Test Number](https://www.twilio.com/docs/iam/test-credentials#test-sms-messages) |

**Hodl Up!** If you're using Test Numbers for Twilio, make sure to use your [Twilio Test Credentials](https://www.twilio.com/console/project/settings)!

## Airtable

| Environment variable name | Description |
| - | - |
| `airtableApiKey` | Airtable API Key. Used for managing the tracking list through Airtable instead of a nested json array. |
| `airtableBaseId` | Your tracking list Airtable Base Identifier. You can find the identifier by visiting [Airtable API Docs](https://airtable.com/api) and clicking on the base you wish to use. |
| `airtableBaseTableName` | OPTIONAL. Your tracking list Airtable Base table name. By default this is `Coins`. |

# Airtable Setup

Instead of manually managing your list through a nested JSON array, you can manage your tracking list through Airtable. 

1. [Create or Sign in to an Airtable account.](https://airtable.com/login)
1. Create a new Airtable base (grid) like below (click to zoom in), set the [Base Id](https://airtable.com/api) as `airtableBaseId` in your environment.
1. Set the Airtable base table name to `Coins` if you'd like another name set `airtableBaseTableName` to the name you've chosen.
1. Generate an [Airtable API Key](https://airtable.com/account) and set `airtableApiKey` in your environment.

[![Imgur](https://i.imgur.com/apxajc5.png)](https://i.imgur.com/apxajc5.png)

## Base Columns

| Column Name | Description |
| - | - |
| coinGeckoId | String. You can obtain a [CoinGecko](https://www.coingecko.com/en) ID by visiting the CoinGecko website, searching for the coin you'd like to track, and copying the end of the url (e.g. coingecko.com/en/coins/**dogecoin**). |
| minimumThreshold | Number (Decimal). When the price of the coin goes below this value an SMS will be sent notifying the user the price is below minimum threshold. <br /><br />When **EMPTY** this check will be skipped. |
| maximumThreshold | Number (Decimal). When the price of the coin goes above this value an SMS will be sent notifying the user the price is above maximum threshold. <br /><br />When **EMPTY** this check will be skipped. |

# Obtaining a CoinGecko ID

1. Go to [CoinGecko](https://www.coingecko.com/en)
1. Search and navigate to the Coin you'd like to track (e.g. BTC)
1. The identifier is at the end of the url (coingecko.com/en/coins/**bitcoin**)

# Running

Now that you've setup your environment variables you're ready to get started. Let's verify that everything works by running the collection:

1. Click "Run"
1. Click "Run Crypto Tracker"

If everything looks good, it's time to setup a [monitor](https://learning.postman.com/docs/designing-and-developing-your-api/monitoring-your-api/intro-monitors/)!