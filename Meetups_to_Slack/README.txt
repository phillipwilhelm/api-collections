Pipe upcoming meetup events to a Slack notification.

Web-viewable collection documentation is published [here](https://documenter.getpostman.com/view/1559645/RWTfxgQ7).

1. Get upcoming meetups related to keyword "Postman".
2. Send a message about any upcoming meetups via a Slack webhook. Instead of Slack, this step can be customized to your specific chat or notification platform.
3. Update your environment to store the state of all the previous meetups. This step is especially useful when scheduling periodic checks for new events.

### Get Started

To run the requests in the first folder, update the following required [environment variables](https://www.getpostman.com/docs/v6/postman/environments_and_globals/intro_to_environments_and_globals).

| Environment variables | Required | Description                                                   |
|------------------------|----------|---------------------------------------------------------------|
| `meetupKey`      | required | Meetup API requires [an API key](https://secure.meetup.com/meetup_api/key/) to access their endpoints            |
| `slackWebhook`                | required | Slack provides [incoming webhooks](https://api.slack.com/incoming-webhooks) to post messages from apps into Slack |

To run the requests in the second folder, update the required [environment variables](https://www.getpostman.com/docs/v6/postman/environments_and_globals/intro_to_environments_and_globals).

| Environment variables | Required | Description                                                   |
|------------------------|----------|---------------------------------------------------------------|
| `postman_api_key`      | required | Generate your key from the [Postman web dashboard](https://app.getpostman.com/)               |
| `current_environment_name`                | required | We will use the [Postman API](https://docs.api.getpostman.com/) to identify your environment's ID |

### Run the collection

* Collection runner: To run the collection one time, use the [Postman collection runner](https://www.getpostman.com/docs/v6/postman/collection_runs/starting_a_collection_run). 
* Automated collection runs: To run the collection on a scheduled frequency, use a [Postman monitor](https://www.getpostman.com/docs/v6/postman/monitors/setting_up_monitor) or use [Postman's command line tool Newman](https://www.getpostman.com/docs/v6/postman/collection_runs/command_line_integration_with_newman) with a cron job.