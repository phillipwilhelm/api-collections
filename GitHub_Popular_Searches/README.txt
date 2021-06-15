A collection to discover popular repositories on [GitHub](https://github.com) for a given search query.

> Set the following environment variables before you run this collection : 
- **{{searchTerm}}** : the query you want to search
- **{{maxSize}}** : maximum number of repositories you want to fetch

It sends the popular repository on Slack channel using webhook.

> This collection uses [Github API](https://developer.github.com/v3/) to fetch comments and sends a report to an internal Slack channel using a [webhook](https://api.slack.com/incoming-webhooks#sending_messages).