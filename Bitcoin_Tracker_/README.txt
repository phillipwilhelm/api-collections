The Bitcoin Tracker is a Postman collection that compares the current Bitcoin exchange rate with a target value. If the current Bitcoin rate drops below this target (like in a flash crash), you will receive an SMS alert.

You can run the collection locally with the Postman collection runner or [Newman](https://www.getpostman.com/docs/v6/api_testing_and_collection_runner/newman_intro) command line tool, or run the collection on the Postman cloud with a [monitor](https://www.getpostman.com/docs/v6/postman/monitors/intro_monitors).

**Legal disclaimer:** Cryptocurrencies are volatile. Postman assumes no ownership (or liability) in all the $$$ you make (or lose). Gamble responsibly!

**To make money:** Running this collection once or twice won't help you make it rain ????. If you're using a Postman monitor, set the frequency to run this check periodically. If you're using the Newman command line tool, write a shell script to set up a cron job that runs the collection periodically.

### Quickstart

Before you can run the Bitcoin Tracker collection, you need to [create or update an environment](https://www.getpostman.com/docs/v6/postman/environments_and_globals/manage_environments). Add the following required variables to a new environment, or update the `Bitcoin Tracker.template` environment you downloaded with the **Run in Postman** button:

|Environment Variable Name |Description
|--------------------------|--------------
|`twilioAccountSID`            |A [Twilio Account SID](https://www.twilio.com/console/project/settings)
|`twilioAuthToken`        |A [Twilio Auth Token](https://www.twilio.com/console/project/settings)
|`targetRate`                |Set a target rate. If the current Bitcoin rate drops below this target, the `POST` request to the Twilio API will be called.

### Twilio credentials

You will need a [Twilio Account SID](https://www.twilio.com/console/project/settings) to add or update the `twilioAccountSID` value within the Postman environment. You will need a [Twilio Auth Token](https://www.twilio.com/console/project/settings) to add or update the `twilioAuthToken` value within the Postman environment.

![[twilio console](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/twilioAuth_censored.jpg)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/twilioAuth_censored.jpg)

### Enter a target rate

You will need to set a target rate by adding or updating the `targetRate` value within the Postman environment. If the current Bitcoin rate drops below this target, the `POST` request to the Twilio API will be called.

