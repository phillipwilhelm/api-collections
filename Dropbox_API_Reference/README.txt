The powerful, yet simple, Dropbox API allows you to manage and control content and team settings programmatically and extend Dropbox capabilities in new and powerful ways. This is a collection that includes requests to all endpoints in the Dropbox API. 

The Dropbox API is divided in two groups of endpoints: User Endpoints and Business Endpoints. Operations that would most likely be executed by a user, such as file operations, are in the User Endpoints folder. Operations that would most likely be executed by a team administrator, such as adding users to groups, live in the Business Endpoints folder. 

If you are new to Dropbox Business and Team Administration, please have a look at the [Dropobox Admin Guide](https://help.dropbox.com/guide/admin/how-to-get-started#dropbox-admin-guide). 

If you want more information on how to use our API please refer to our [Developer Portal](https://www.dropbox.com/developers). 

# What's in the collection?

The endpoints are organized in the following folders:
* account
* auth
* check
* contacts
* file_properties
* file_requests
* files
* sharing
* team
* team_log
* users

# Authorization

## OAuth 2.0 for API Access
Dropbox uses OAuth 2.0, an open specification, to authorize access to data. To get an OAuth token from Dropbox to enable Postman to access your Dropbox account via the API you’ll need to create a new app on the DBX Platform.

## Creating an App on the DBX Platform
Navigate to https://www.dropbox.com/developers/apps and select “Create app” 
1. Choose an API  
2. Choose the type of access you need 
3. Give your app a name  
4. Choose the Dropbox account that will own your app  

For reference, please use the [Dropbox OAuth guide](https://www.dropbox.com/lp/developers/reference/oauth-guide) 

## Generating an Access Token
Once you select “Create app” a page will load that displays information about your newly created app. To generate an access token scroll down to “OAuth 2” and click “Generate” beneath “Generated access token.” The token will display as a long string of characters. Copy this token for use with the Postman Collection.

## Adding an Access Token to the requests
In the Postman client, click on the three dots to the right of the collection name to "View more actions."

![Screenshot of adding access token](https://www.dropbox.com/s/sfebu9ai76cbq39/Screen%20Shot%202020-10-28%20at%2012.50.56%20AM.png?raw=1)

Then, click "Edit."

Click on the "Variables" tab and, in the row for the `access_token` variable, paste your access token in the `CURRENT VALUE` column. The default value is `your-access-token-here`.

![Screenshot of adding access token](https://www.dropbox.com/s/ahnbxwe6oscjues/Screen%20Shot%202020-10-28%20at%2012.51.13%20AM.png?raw=1)

For information on sessions and variables in Postman see the blog post at https://blog.postman.com/sessions-faq/.

# Notes
* Dropbox also has a Postman Collection in the API Network to help administrators with team management workflows. It is called [Dropbox Team Admin Workflows](). 

