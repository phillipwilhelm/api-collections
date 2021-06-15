The powerful, yet simple, Dropbox API allows you to manage and control content and team settings programmatically and extend Dropbox capabilities in new and powerful ways. One of the many areas where the Dropbox API shines is Team Administration. Dropbox Business brings collaboration to professional teams of all sizes, with all the security and control that is required. 

If you are new to Dropbox Business and Team Administration, please have a look at the [Dropobox Admin Guide](https://help.dropbox.com/guide/admin/how-to-get-started#dropbox-admin-guide). 

# Why would you need these workflows?  

Many of the administration tasks can be executed through the web-based Admin Console. However sometimes our Dropbox Business customers need to perform tasks in bulk or automate actions, in a way that is only possible via the API. Furthermore, to accomplish some of these goals it is required to chain a few API calls (the response of a call is the input for the subsequent call), or loop through a list.  

That's why we created the Dropbox Team Admin Workflows Postman Collection. It is aimed at helping Dropbox Administrators on specific tasks, but it can also help developers learn about our APIs. Each folder contains specific workflows that include multiple endpoints that are connected to accomplish specific tasks. 

If you want more information on how to use our API to manage your Dropbox team, please refer to the [Dropbox API Team Administration Guide](https://www.dropbox.com/lp/developers/reference/dbx-team-administration-guide).

# What's in the collection?

These are the workflows contained in this collection:  

**Bulk Provision Users and Add to Groups**  
Create users from a list and add them to appropriate groups  

**Bulk Deprovision Members with Transfer Destination**  
Remove members from a list and transfer their personal data  

**Bulk Deprovision Members without Transfer Destination**  
Remove members from a list and their personal data  

**Bulk Suspend Members**  
Suspend a list of members  

**Bulk Unuspend Members**  
Unsuspend (reactivate) a list of members  

**Bulk Add Users To Groups**  
Add a list of users to appropriate groups  

**Bulk Update Email Addresses**  
Update email addresses for a list of users  

**Bulk Add Groups**  
Create groups from a list  

**Wipe External ID**  
Wipe the External ID field for all users in a team  

**Bulk Update External IDs**
Update specific External IDs using a CSV file

Each workflow has its own folder. Please visit the folder description for instructions on how to execute it. Some workflows require CSV (comma-separated values) files with the input lists. Those formats are in the descriptions, along with links to sample files you can download and use. 

# Authorization

## OAuth 2.0 for API Access
Dropbox uses OAuth 2.0, an open specification, to authorize access to data. To get an OAuth token from Dropbox to enable Postman to access your Dropbox Business team via the API you’ll need to create a new app on the DBX Platform.

## Creating an App on the DBX Platform
Navigate to https://www.dropbox.com/developers/apps and select “Create app” 
1. Choose an API  
2. Choose the type of access you need 
3. Give your app a name  
4. Choose the Dropbox account that will own your app  

For reference, please use the [Dropbox OAuth guide](https://www.dropbox.com/lp/developers/reference/oauth-guide) 

## Generating an Access Token
Once you select “Create app” a page will load that displays information about your newly created app. To generate an access token scroll down to “OAuth 2” and click “Generate” beneath “Generated access token.” The token will display as a long string of characters. Copy this token for use with the Postman Collection.

## Adding an Access Token to the Postman Collection
In the Postman client, click on the three dots to the right of the collection name to "View more actions."

![Screenshot of adding access token](https://www.dropbox.com/s/39kae4jmnjab3dd/Screen%20Shot%202020-07-17%20at%2012.29.33%20AM.png?raw=1)

Then, click "Edit."

![Screenshot of adding access token](https://www.dropbox.com/s/8nprpathnaxag74/Screen%20Shot%202020-07-17%20at%2012.29.57%20AM.png?raw=1)

Click on the "Variables" tab and, in the row for the `access_token` variable, paste your access token in the `CURRENT VALUE` column. The default value is `your-access-token-here`.

![Screenshot of adding access token](https://www.dropbox.com/s/jbd1g3843gviylr/Screen%20Shot%202020-07-17%20at%2012.30.12%20AM.png?raw=1)

For information on sessions and variables in Postman see the blog post at https://blog.postman.com/sessions-faq/.

# Notes
* We use Collection variables for storing values in between requests, as well as input values. Please visit each workflow folder for instructions on how to provide values for these variables.   
* You can find the CSV templates for the workflows [in this folder](https://www.dropbox.com/sh/3thw4wqwn7o07kh/AABug6oNSL7Vxj98fZ6Hnwoka?dl=0).
