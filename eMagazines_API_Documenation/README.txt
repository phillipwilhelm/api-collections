The eMagazines Digital Fulfillment (EDF) API makes partner integration simple. For the turn-key set-up, the only API call needed is Subscribe – the EDF system handles the rest, from sending the initial order confirmation, to emailing next-issue notifications, to hosting a digital library of past issues.
The EDF API was designed to be flexible, supporting partners who wish to email notifications through their own ESP, host a customer’s digital library on their own website, and set up their own customer service tools to manage users and subscriptions.
The API also supports archive partners that wish to permission consumers for all-access passes (all issues across the history of a title).

Restful API

The EDF API is a restful API that accepts HTTP POST requests. API end-points include Subscribe, Cancel, Issue, Library, Reset, Customer, All-Access and Archive.
Both requests and responses take the form of a simple JSON dictionary object. For example, this is a Subscribe call to a test program:

{
"Key":"3127620F-9C5B-4393-B849-53B6A0ADA280",
"ProgramKey":"pub_test_12_email",
"Email":"customer@emagazines.com"
}

Responses always include a status and message, plus the requested payload fields. This is an example of a Subscribe response:

{
"status":"ok",
"message":"successful subscription",
"entitlement_link":"”,
"latest_issue_link":"”,
"library_link":"”
}

See the accompanying test HTML app to see all the API calls in action and try them out for yourself.
