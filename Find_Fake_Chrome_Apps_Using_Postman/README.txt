This collection finds fake or malicious apps in chrome web-store which pretend to be someone else. 

The collection has two folders,

1. The first folder simulates a search query in chrome web-store. It collects all the search results for _your app name_ and reports fake or malicious app via Slack channel.
2. Second folder search for _your app name_, using a custom google search engine APIs. Results are reported through Slack in a slack channel. Security team verify apps in the results and put them in the whitelist.


In the environment variable you've to provide information about your app such as app/extension title, developer name, and in description. The description contains keywords describing _your app_. Use below description to edit environment variables.

- `app_title`: Your application title, same as in Chrome web-store.
- `app_developer`: Developer name, same as in Chrome web-store.
- `app_keywords`: A list of keywords that describes your app.
- `search_api_key`: An API key for Google custom search engine.
- `cx`: Google custom search engine ID.
- `slack_webhook_url`: Slack Webhook URL.