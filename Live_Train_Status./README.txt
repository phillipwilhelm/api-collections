Live Train Status is a Postman Collection which can be used to check the PNR status of the train ticket and can also be used to track the live running status of a train. Complete status is send as an alert to slack using [Slack's Incoming Webhook](https://api.slack.com/incoming-webhooks). It can be run locally with the postman collection runner, but it's best to run the collection using the slash command in slack. Specifying the PNR no along with slash command can be used to run the complete collection and getting the required output on the slack.

<h2> QUICKSTART </h2>

Before running the <b>Live Train Status</b> postman collection, it requires to [create or update an environment](https://learning.getpostman.com/docs/postman/environments_and_globals/manage_environments/). Add the following variables to a new environment, or update the values of these variables by choosing the 'train' environment.

|Environment Variable name:|	
|------------------------|
|trainapikey = An API key which can be [generated](https://indianrailapi.com/dashboard/api-key).| 
|pnrno<b>[Optional]</b> = Specifies the PNR no of the journey. Passing PNR no through slash command do not require to set it as an environment variable.|
|incoming_webhook = Specifies the slack's Incoming Webhook URL which is used to send final response to slack. This can be set up from [Slack's Incoming Webhook](https://api.slack.com/incoming-webhooks).|


<b>Setting Up Slash Command</b><br>
Slash Command is basically a way to pass inputs to a postman collection. [To set up a Slash Command](https://api.slack.com/slash-commands) requires a URL of the postman collection.

URL of the postman collection can be generated from the response of this <b>POST request:</b><br> <a>https://api.getpostman.com/webhooks?apikey={{postman_api_key}}</a>

Body of this request:
<pre>
{
	"webhook": {
		"name": "Live Train Status.",
		"collection": "{{collection_uid}}",
		"environment": "{{environment_uid}}"
	}
}
</pre>
After the Slash command has been set up. Collection can be executed by passing the 10-digit PNR number along with the slash command and it start executing the requests.

<h2>API's Used </h2>
Indian Rail API,
 Slack API
and Postman





