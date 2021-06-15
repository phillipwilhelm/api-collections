This collection helps initiate a Secret Santa gift exchange through a specified slack channel for a particular budget. It also gives gift recommendations based on the interest of the person you were assigned.

**Setup**

To run this collection locally, you will need an environment with the following variables:

1. `budget` : denotes the spending cap for all participants in the gift exchange in numbers
2. `channel`: denotes the Slack channel name whose members will be participating in Secret Santa
3. `amazonUrl`: denotes the Amazon base url for your region
4. `botToken`: denotes the token of the bot user created in [Slack](https://slack.com/intl/en-in/help/articles/115005265703-create-a-bot-for-your-workspace)
5. `googleClientId`, `googleClientSecret` :  specifies your Google API Oauth Client credentials that need to be [generated](https://accounts.google.com/signin/v2/identifier?service=cloudconsole&passive=1209600&osid=1&continue=https%3A%2F%2Fconsole.cloud.google.com%2Fapis%2Fcredentials%3Fref%3Dhttps%3A%2F%2Fwww.google.com%2F&followup=https%3A%2F%2Fconsole.cloud.google.com%2Fapis%2Fcredentials%3Fref%3Dhttps%3A%2F%2Fwww.google.com%2F&flowName=GlifWebSignIn&flowEntry=ServiceLogin)