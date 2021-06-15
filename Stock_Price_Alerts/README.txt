This is a Postman Collection demo, which can help users monitor (US) stock prices and trigger threshold-based alerts sent to Slack (only lower-threshold alerts are implemented in the demo).

You can enter and modify kicker symbols, company names, and alert thresholds for stocks you track in a Airtable spreadsheet-like data table. You will see alerting messages in a Slack channel you define or in your personal message window, as they are triggered. 

In addition to the collection, the following variables are defined in a Postman Environment. 

- slack_webhook_url 
- stock-api-token //you can get this token from the stock API provider you choose to use.
- airtable_api_key
- airtable_stocks_table_id

 