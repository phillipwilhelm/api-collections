### Intro

Follow along with this blog post: **[Scripting an Airtable to SurveyMonkey uploader]()**.

The [SurveyMonkey API documentation](https://developer.surveymonkey.com/api/v3/) has a **Run in Postman** button documenting all of their endpoints. Import their entire Postman collection into the Postman app to get started quickly.

The [Airtable API documentation](https://airtable.com/api) has an easy way to access your Airtable data. If you don't already have an airtable base, you can use [this example](https://airtable.com/shry9zUrZ2gacyYQf) and follow along.

### Get Started

[Update the environment](https://www.getpostman.com/docs/v6/postman/environments_and_globals/manage_environments#editing-an-active-environment) with your own authorization credentials.

| Required Environment Variables | Description  |
|------------------------|-------------|
| `airtable_base` | Review the automatically-generated [Airtable API documentation](https://airtable.com/api) for your own airtable base. |
| `airtable_api_key` | To generate or manage your API key, visit your [Airtable account](https://airtable.com/account) page. |
| `surveymonkey_token` | Create [a new SurveyMonkey app](https://developer.surveymonkey.com/apps/), select scope permissions, and get the access token. |
| `SURVEY_ID` | Use the SurveyMonkey API documentation to `GET` this information. |
| `PAGE_ID` | Use the SurveyMonkey API documentation to `GET` this information. |

### Run the collection

This operational collection works like a script or utility, and will continue to iterate over every airtable record and create a new question until there are no more questions left. 

* **Controlling your workflow:** we can use [`postman.setNextRequest()`](https://www.getpostman.com/docs/v6/postman/scripts/branching_and_looping) to continue sending the same request until no more questions remain.
* **Saving state:** we can use an [environment variable](https://www.getpostman.com/docs/v6/postman/environments_and_globals/intro_to_environments_and_globals) like `airtable_records` to save the current state of the array containing all the questions that remain to be uploaded.

