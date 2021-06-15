#### A monitor to summarise GitHub activity of last day pertaining to issue sentry

![github-support-issues-alert-screenshot](https://user-images.githubusercontent.com/5207331/29210371-f0f51f64-7eb0-11e7-8f7e-5793b5649961.png)

Every day, issues reported on GH needs the following:
1. Label
2. Assignee
3. Initial reply from Postman team

This collection uses [Github API](https://developer.github.com/v3/) to get support issues and sends a report to an internal Slack channel using a [webhook](https://api.slack.com/incoming-webhooks#sending_messages).

### Quickstart

To get started, [update these environment variables](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments#edit-an-active-environment).

#### Environment variables required
- __gh-api-token__: Github API Token (with read:org scope)
- __slack-webhook__: Slack Webhook URL

Get your [GitHub API token](https://github.com/settings/tokens/new).

![github-token-screenshot](http://i.imgur.com/XBjx9X6.png)

Set up your [Slack incoming webhook](https://my.slack.com/services/new/incoming-webhook/).

![slack-webhook-screenshot](http://i.imgur.com/9JDKfxd.jpg)

Once you've updated these 2 environment variables, you're ready to run the collection.

The general workflow for the collection:

![request workflow](http://i.imgur.com/IK1Tt0d.png)