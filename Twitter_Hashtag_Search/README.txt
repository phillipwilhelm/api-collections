## About

This is a parent folder for the Postman Collection created to search for hashtagged tweets and post them to Slack. 

Before this collection will work as expected, we need to input some important authorization credentials.

### READ THE BLOG POST
- [Part I: How to Use the Twitter API to Build a Hashtag Search Bot](https://blog.postman.com/how-to-use-twitter-api-create-hashtag-search-bot/)

### CHECK OUT THE LIVESTREAM
- [Part I: Finding the hidden gems in the Twitter API](https://youtu.be/ySbLo13Fk-c)
- [Part II: The Twitter API: Confessions of a User](https://blog.postman.com/twitter-api-confessions-of-a-user/)

#### Quickstart
If you want to get started immediately without reading through the detailed documentation, here are the quick and dirty steps:
1. Fork this collection into your own workspace.
2. Fork the [`Twitter Hashtag Environment`](https://www.postman.com/postman/workspace/published-postman-templates/environment/13455110-f36b644a-a69f-4768-ba20-763c806e0d9d) environment into your own workspace.
3. Enter the missing auth credentials in the environment (Twitter bearer token, Postman API key, and Slack webhook URL).
4. Change the `query` param in the "Search for Hashtag" request.
5. Create a Monitor for the collection.
6. Check out the Slack messages!

## Detailed Steps

#### Fork this workspace
If you want to work with this collection yourself, click the "Fork" button on the top right section of Postman and select your own workspace as the destination for the fork. This will allow you to customize the requests and run through the collection yourself.

#### Fork the environment
To save some time of manually creating an environment and copying/pasting variable names, you can simply fork the environment directly from this workspace into your own. Similar to the steps above for forking a workspace, follow the same steps for the environment. Click the environments section in the top right, select "Twitter Hashtag Environment", then click "Fork". 

You can also directly go that environment (here)[https://www.postman.com/postman/workspace/published-postman-templates/environment/13455110-f36b644a-a69f-4768-ba20-763c806e0d9d].


#### Twitter requirements
You will need to obtain a bearer token from Twitter. Go to your [developer dashboard](https://developer.twitter.com/en/portal/projects-and-apps), and find the Projects & Apps section. If you haven't created a new App/Project, you must do that first. Once that is complete, copy the bearer token value and paste it into your environment variable.

#### Postman requirements
Next you'll need a valid [API Key](https://postman.postman.co/workspace/Twitter-Workspace~a2ae0092-a8f5-412f-9c41-b009fda1e633/collection/12959542-c8142d51-e97c-46b6-bd77-52bb66712c9a?ctx=documentation#authentication) to send requests to the API endpoints. You can get your key from the [integrations dashboard](https://go.postman.co/settings/me/api-keys).

The API Key is required to be sent as part of every request to the Postman API, in the form of an X-Api-Key request header. 

Once you find your Postman API Key, save the value as the environment variable `postman_api_key`.

#### Slack requirements
In order to send the messages to Slack, you need to have a url to send a POST request to. You can do this by following the instructions on [Getting started with Incoming Webhooks](https://api.slack.com/messaging/webhooks) Step 3 & 4 of those instructions will explain how/where you get the required URL.

Once you have the webhook URL, copy it and paste it into the environment variable `slack_webhook_url`.


#### Automating the workflow
To have this collection run at set intervals, you'll need to create a [monitor](https://learning.postman.com/docs/designing-and-developing-your-api/monitoring-your-api/intro-monitors/) by clicking the "Monitors" icon on the left side of the screen.  Make sure to select the correct Environment for your monitor. The workflow when automated looks likes this:
![An example workflow](https://i.imgur.com/QP7j7te.png "Here's the workflow.")


#### Credit
The code in the Pre-request Script page is duplicated from [Twitter's Public Workspace](https://www.postman.com/twitter/workspace/twitter-s-public-workspace/overview).. It lays the foundation for the requirements necessary for accessing the Twitter API v2.