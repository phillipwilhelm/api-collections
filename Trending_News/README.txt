Do you look at Twitter hash tags and not understand the context behind them? Do you find yourself clueless when it comes to trending topics? This collection is for you.

It will pull the trending hash tags off Twitter and match them with corresponding news articles. These news articles will then be pushed to the slack channel of your choice. Don't want others to read your articles? You can push them to your own private chat too.

Setup:

1. We need to setup a Twitter App to use the Twitter API - [Getting Started](https://developer.twitter.com/en/docs/basics/getting-started)

2. We will be using Application-only authentication for this Collection - [Application Only Auth](https://developer.twitter.com/en/docs/basics/authentication/overview/application-only)

3. Once we create the Twitter App we will need to fetch the Consumer API Key and Consumer API secret key. Add them in the environment as `CONSUMER_API_KEY` and `CONSUMER_API_SECRET` respectively.

4. We will need to add the `NEWS_API_KEY` from [newsapi.org](newsapi.org)

5. And, `SLACK_HOOK` which is the Webhook to the Slack channel you want the news articles posted to.

6. Finally, we set `NUMBER_ARTICLES` to the maximum number of articles to be pushed to Slack