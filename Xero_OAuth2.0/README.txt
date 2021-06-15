## Steps to get up and running
Follow these steps to quickly get up and running with the Xero API and Postman:

### 1. Create an app at https://developer.xero.com/myapps
Go to the Xero developer portal and create an OAuth2 app.

If you haven't already signed up for a xero account you can do so [here](https://www.xero.com/signup/api/).

Use the following values:
* App Name - your choice, but can't contain the word 'Xero'
* Company or application URL - this needs to be an https address, but isn't used.
* OAuth 2.0 redirect URI - this needs to be https://oauth.pstmn.io/v1/browser-callback

Then:
1. Click Create App
1. Click Generate a secret
1. Keep the page open

### 2. Add your first set of environment variables in Postman
Copy the Client id and Client secret from the My Apps screen into the environment variables in Postman. To add these details to the Environment, make sure you have the OAuth 2.0 Environment selected, click the eye button, then edit.

Add the scopes required to the `scopes` environment variable. 
Our Developer Center lists the available scopes [here](https://developer.xero.com/documentation/oauth2/scopes). For getting started you will need at least:

`offline_access accounting.transactions`

In addition, to make further test calls we would also suggest adding:

`openid profile email accounting.contacts accounting.settings`

### 3. Generate your access token
1. Click on the GET Connections request under the Xero OAuth 2.0 Collection
1. Select the Authorization tab
1. Click Get New Access Token

At this stage you will be prompted to log in to Xero. 

You'll then be taken through to the Organisation select and consent screen. Select the Organisation you want to connect to. If you want to connect to more than one Organisation, you can repeat the steps above and select another Organisation. 

Once complete you'll be passed back to Postman.

### 4. Set your Access and Refresh Tokens
We now have the last remaining tokens needed to access the Xero API. These need to be set to the Environment Variables, to do this:
1. Copy and paste the access token and refresh token somewhere (e.g. a text file).
1. Set them as environment variables
1. Delete the text file

The reason we save them as environment variables (rather than using Postman's in-built token management) is so we can refresh them using the Refresh token request.

### 5. Find out which tenants (organisations) we are connected to

1. Click Send on the GET Connections request
1. The tenantId from the first connection in the list will be saved to the xero-tenant-id environment variable. If you want to use a different tenant you can manually change that environment variable. 

Congrats! You're now authenticated and can start making API calls. Your access token will last for 30mins, after which time you'll need to refresh the token. 

### 6. Make your first API call!
1. Click to load the GET Invoices request
1. Ensure No Auth is set on the Authorization tab (your access token variable is manually added to the headers)
1. Click Send

### 7. Refreshing the token
1. Click to load the POST Refresh token request
1. Ensure No Auth is set on the Authorization tab (your access token variable is manually added to the headers)
1. Click Send

### Notes:
* We use the built in OAuth 2.0 support to get the token, however we then set this as an environment variable. So we don't need to use this support when making the normal API calls.