Amazon book price tracker is a Postman Collection that can track price of a particular book on amazon.in. When run it searches the book on amazon and notifies the user through slack when the price reduces. It can be run locally with the postman collection runner, but it's best to run the collection as a scheduled job with [Postman Monitor](https://learning.getpostman.com/docs/postman/monitors/intro_monitors/).
You can set the book's name with environment variables, and it stores the price and other details about the book to a environment for future use, and to check next time if the price has decreased or not.

# Before starting
---
Before you can run the collection, you need to create an environment. Add the following required variables there.
<table>
	<tr>
		<th>Name of the variable</th>
		<th>Initial value</th>
	</tr>
	<tr>
		<td>book name</td>
		<td>The book's name</td>
	</tr>
	<tr>
		<td>slack_webhook_url</td>
		<td> Link to your slack apps <a href="https://api.slack.com/incoming-webhooks#enable_webhooks">webhook</a></td>
	</tr>
	<tr>
		<td>apikey</td>
		<td>Your api key for using Postman Api, get it from <a href="https://go.postman.co/integrations/services/pm_pro_api">here</a></td>
	</tr>
	<tr>
		<td>env uid</td>
		<td>The unique id of the environment that you created</td>
	</tr>
</table>


## Get the slack webhook url

Log in to your team Slack account and [create a Slack app](https://api.slack.com/slack-apps). Then [activate and configure an incoming webhook](https://api.slack.com/incoming-webhooks) for your app. Add this webhook url as `webhook` in your environment.

## Get the Postman Api key

You need a valid API Key to send requests to the API endpoints. You can get a key in the [Integrations](https://app.getpostman.com/dashboard/integrations) page.

## Get the environment unique id

Once you've created your environment, you can get the `env uid` value by downloading the environment and copying the id from the environment file.


## Add the `book name`


Now as all the setup is done, now you need to edit the `book name` environment variable to the book's name you want to track the price of. And the name should be accurate otherwise it may get incorrect result.