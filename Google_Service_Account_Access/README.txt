# Automating Google API with Monitors

The hardest thing about OAuth2.0 for automation is a consent screen. 
OAuth2.0 is a very popular way to sign into applications to have them access data which leaves elsewhere. This becomes an issue if you want to automate tasks in Google Docs. 

This can be solved however with Google Service Accounts. 

Create a Google Service Account in https://console.developers.google.com
Create Credentials > Service Account Key 

Grab the private key from the donwloaded JSON file and store it as an environment variable called  `privateKey` 

Any resource in Google Drive, you want to the service account to have access to, share the resource with the service account email. 
