Look up all DNS records for a domain and get notified about the status and records by an incoming slack webhook.


You can setup a monitor to notify your team the DNS Records for your domain via Slack.


This can also be used to check if a domain is valid or not.


The documentation of the collection also explains the DNS concepts involved.

The run makes use of Postman Echo, `pm.sendRequest` in test scripts and re-using code in tests by doing an `eval` of the code stored in environment variables aka collection level scripts.

You have to provide two optional variables as input:

1. `domain`: The domain you want to check your DNS records for (Defaults to getpostman.com)
2. `slack_incoming_webhook`: An endpoint where you will receive the details about the DNS records. Could be any webhook, the data will just be HTTP POSTed to this endpoint in the Slack Message Format. If nothing is provided, no Slack notifications will be sent. You will have to inspect the monitor run console log to view the output.