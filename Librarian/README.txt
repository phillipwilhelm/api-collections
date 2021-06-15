Librarian is a [Postman collection](https://www.getpostman.com/docs/postman/collections/creating_collections) that allows you to use Slack to check the availability of a book in your office library. In this case, we are searching for the book using a Slack app, and also storing the books that we have in the Postman office using [Airtable](https://airtable.com/) as a database.

[![GIF of searching in slack](https://jsshzyxacm.files.wordpress.com/2017/10/search-for-a-book4.gif)](https://jsshzyxacm.files.wordpress.com/2017/10/search-for-a-book4.gif)

Review the [collection documentation](https://documenter.getpostman.com/view/804329/71FWAgx) for more details.

# Search in Slack

You can search for your book by typing `/bookbug [book-name]` in Slack. No switching applications or learning a new UI!

[![Image of searching in slack](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-4-05-40-pm-e1513001141402.png)](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-4-05-40-pm-e1513001141402.png)



* If the book is up for grabs, you will see the details of the book -
[![Image of book available](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-5-41-20-pm.png)](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-5-41-20-pm.png)



* If the book is with someone, you will know who is reading it currently-
[![Image of currently reading](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-5-54-59-pm.png)](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-5-54-59-pm.png)



* If the book is unavailable, well, it is time to buy a new book -
[![Image of unavailable](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-5-57-51-pm.png)](https://jsshzyxacm.files.wordpress.com/2017/10/screen-shot-2017-10-23-at-5-57-51-pm.png)


----
# How it works

When you type `/bookbug [The Hobbit]` in Slack and hit enter, the message (and its data) is sent to the configured external URL (Postman monitor url in our case) via `HTTP POST`. The monitor starts the "Librarian" collection run.


[![Image of how it works](https://jsshzyxacm.files.wordpress.com/2017/10/librarian-slack-app.png)](https://jsshzyxacm.files.wordpress.com/2017/10/librarian-slack-app.png)


# Getting Started


## Create an Airtable base (database)

Create an [Airtable base](https://support.airtable.com/hc/en-us/articles/202576419-Introduction-to-Airtable-bases) with the schema similar to [this base](https://airtable.com/shrSgSkkOcWGdlJ8F). Airtable provides a nice graphical interface to add entries to the base. You can also click on "Copy base" on the top right of [this base](https://airtable.com/shrSgSkkOcWGdlJ8F) to create a copy for yourself. We will use the [Airtable API](https://airtable.com/api) to query this base.


## Create a Slack app (frontend)

Log in to your team Slack account and [create a Slack app](https://api.slack.com/slack-apps). Then [activate and configure a slash command](https://api.slack.com/slash-commands) and **install this app** to your Slack workspace. You will need to enter the Postman monitor URL which we will create below in the `Request URL` text box.


## Run in Postman

Click the orange [Run in Postman button](https://www.getpostman.com/docs/postman_for_publishers/run_button/creating_run_button) to import the sample collection and environment template into your Postman app. Before you can run the Librarian collection, you need to update the `Librarian.template` [environment](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments) you downloaded with the *Run in Postman* button. Add appropriate values to the variables:

|Environment Variable Name |Description
|--------------------------|--------------
|`airtable_api_key`            |[An Airtable API Key.](https://support.airtable.com/hc/en-us/articles/219046777-How-do-I-get-my-API-key-)
|`airtable_url`        |Request url. Select your base from [here](https://airtable.com/api). Each base can contain multiple [tables](https://support.airtable.com/hc/en-us/articles/202576419-Introduction-to-Airtable-bases), so you will have to navigate to your specific table in the left sidebar. The `airtable_url` will be the curl in the "Example Request" for "Retrieve a record".                                                        [![Image of airtable_url](https://jsshzyxacm.files.wordpress.com/2017/10/airtable-url.png)](https://jsshzyxacm.files.wordpress.com/2017/10/airtable-url.png)


## Create a Postman monitor

There are currently 2 ways to run a Postman monitor *on-demand*. You can manually run a monitor from the [Postman web dashboard](https://monitor.getpostman.com/), or you can use the [Postman API](https://docs.api.getpostman.com/) to run a monitor, but these methods don't allow you to send a payload. This *on-demand* Postman monitor - which functions like a webhook - will receive the payload sent by Slack and start the "Librarian" collection run.

**Note:**  [Postman webhooks](https://www.getpostman.com/docs/postman/monitors/integrations_for_alerts) are still under development, and not yet recommended for commercial use. 

* Generate an API key from the [integrations dashboard](https://app.getpostman.com/dashboard/integrations) to access the [Postman API](https://docs.api.getpostman.com/). 
* Retrieve all your collections by sending a `GET` request to `https://api.getpostman.com/collections`, and don't forget to add the `x-api-key` header using your Postman API key. Find (**CMD/CTRL + F**) the "Librarian" collection in the response and make a note of the `uid` field. This is your collection ID.
* Retrieve all of your environments by sending a `GET` request to `https://api.getpostman.com/environments`, and don't forget to add the `x-api-key` header using your Postman API key. Once again, find (**CMD/CTRL + F**) the "Librarian" collection in the response, and make a note of the `uid` field. This is your environment ID. 
* Now, let's create a [Postman webhook](https://www.getpostman.com/docs/postman/monitors/integrations_for_alerts). Create a new `POST` request to `https://api.getpostman.com/webhooks`, again adding the `x-api-key` header. For the body, select `raw`, change the type to `JSON`, and add the example body below. Send the request, and copy the `webhookUrl` from the response. We will use this `webhookUrl` in the Slack app configuration as the `Request URL`, essentially telling Slack to run the Postman monitor when the Slack command is triggered.

[![Webhook body](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/webhookUrl.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/webhookUrl.png)