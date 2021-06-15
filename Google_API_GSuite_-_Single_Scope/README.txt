# Postman, GoogleAPI & OAuth2

### a.k.a. The good, the bad, and the ugly. It's up to you how you order the components!

## Summary
Coming from a DevSecOps background I decided that I ought to maintain my infrastructure as code.  
&nbsp;  
To achieve this for [G Suite](https://gsuite.google.com/) one has to utilise the [G Suite GoogleAPI (gAPI)](https://developers.google.com/admin-sdk) which in turn requires [OAuth2](https://aaronparecki.com/oauth-2-simplified/).  

The fun, not to mention the bun fight, begins...  
&nbsp;  
When using OAuth2 with [Postman](https://www.postman.com/) for our personal accounts we really only need 2-legged OAuth but we have to use 3-legged OAuth with gAPI (see the [OAuth2](https://aaronparecki.com/oauth-2-simplified/) link if you need to understand 2 verus 3 legs).  The third leg has to be performed 
manually (although I'm still searching for a solution to that; suggestions welcome).  
&nbsp;  
As I struggled to get this working I thought I was just being dim witted but found that I had actually followed in the hallowed footsteps of no less a deity than [Martin Fowler](https://martinfowler.com/articles/command-line-google.html).  Even his article is now out of date after just nine months thanks to changes in gAPI.  
&nbsp;  
Postman does have a method that automates the process but gAPI tokens only last one hour so you have to manually refresh the token.  
&nbsp;  
**This collection** is for use with a single scope only.  Multiple scopes should work but have failed to do so during my efforts.  In theory you should use the minimum privilege possible so using a collection per scope is no bad thing. However, I am creating a multi-scope collection that will allow all the requests for G Suite administration in one collection.  
&nbsp;  
**The conclusion** I came to is that you cannot use Postman, as great a tool that it is, to fully automate this process.  You are highly recommended to use a full language such as Python, Go, Javascript, [insert your language preference here].  Whichever language you choose, you'll still need to understand these steps first.  
&nbsp;   
The process required is documented below. Steps 1-4 have to be completed manually but, hopefully, only once.  
Step 5 shows how to refresh the `access_token` manually.  The collection uses `pre-request-scripts` to perform this task automatically only when the token has expired.

## Working Steps Version 1

**1) In browser we get a !ONE TIME! CODE :**

G Suite Admin is undertaken via the [Google Cloud Platform console](https://console.cloud.google.com).  You can setup credentials and scopes at the [APIs & Services credentials](https://console.cloud.google.com/apis/credentials?project=gsuite-itp-com) tab.  This will give you the **client_id** used below.
   
  - Single scope - you can have an access_code per scope

  ```
  https://accounts.google.com/signin/oauth?scope=https://www.googleapis.com/auth/admin.directory.group&redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=code&client_id=744399Sani-tisedio43fagg4amsaonind68spa45nk.apps.googleusercontent.com&o2v=1&as=ejH4UFCyT0CRlUh768SBow
  ```
  Change the `scope` to the required access.  Checkout 
  [OAuth 2.0 Scopes for Google APIs](https://developers.google.com/identity/protocols/oauth2/scopes)
  to find the appropriate scope  
&nbsp;  

  - Multiple scopes in theory !!! doesn't work !!! Suggestions welcome

  ```
  https://accounts.google.com/signin/oauth?scope="https://www.googleapis.com/auth/admin.directory.group https://www.googleapis.com/auth/admin.directory.domain"&redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=code&client_id=744399Sani-tisedo43fagg4amsaonind68spa45nk.apps.googleusercontent.com&o2v=1&as=ejH4UFCyT0CRlUh768SBow
  ```

  - **NOTA BENE:** We should only need to get this once and it is seemingly 
  impossible to automate using the GoogleAPI. Thus it is a manual step.
  Once we have a `refresh_token` (see step 4) then we can use that 
  programmatically to update the `access_code` when it expires.  
&nbsp;  

**2) Copy code from browser screen and export:**

  ```
  export CODE="4/1AFMOCUiVByuzjSanitisedqdpdVsdQJm8IcqhUl_GxPkdJycMX8Vo"
  ```
&nbsp;  

**3) Export other variables:**

  ```
  export CLIENT_SECRET="jZ9AWSanitisedQvXHG"                                              # Obtained from https://console.developers.google.com/apis/credentials
  export CLIENT_ID="744399Sani-tisedio43fagg4amsaonind68spa45nk.apps.googleusercontent.com"  # Obtained from https://console.developers.google.com/apis/credentials
  export SCOPE="https://www.googleapis.com/auth/admin.directory.group https://www.googleapis.com/auth/admin.directory.domain https://www.googleapis.com/auth/admin.directory.customer https://www.googleapis.com/auth/admin.directory.group.member https://www.googleapis.com/auth/admin.directory.orgunit https://www.googleapis.com/auth/admin.directory.rolemanagement https://www.googleapis.com/auth/admin.directory.user https://www.googleapis.com/auth/admin.directory.user.alias https://www.googleapis.com/auth/admin.directory.user.security https://www.googleapis.com/auth/admin.directory.userschema https://www.googleapis.com/auth/cloud-platform"
  ```
  - Scope obtained from https://developers.google.com/identity/protocols/oauth2/scopes
  
&nbsp;  

**4) Run the following curl command:**

```
curl -s -X POST \
  -d code=$CODE \
  -d client_id=$CLIENT_ID \
  -d client_secret=$CLIENT_SECRET \
  -d redirect_uri=urn:ietf:wg:oauth:2.0:oob \
  -d grant_type=authorization_code \
  -d access_type=offline \
  -L https://accounts.google.com/o/oauth2/token
```

  This will respond with:
```
{
  "access_token": "ya29.a0AfH6SMAsLAfqnBDish0KGVzxV4gVjU1XgofQQRnaE8mNV4S9djg7RMbC4BgYEv23ENBQXH8YsXL3pr8Qy0yKSImJc1yAi6wXukQkZrvEEHanDmxxcjpyglg_KmaY4HXgWk0nccvhf8NrBqWi5JzSVoo-ev_50d4Z7Lo",
  "expires_in": 3599,
  "refresh_token": "1//03omSg5YlxYZnCgRAAG-you're-nuts-if-you-think-I-haven't-sanitised-this-J6scO7bNzJwhKqh3f2mI_gFVqu9bQ",
  "scope": "https://www.googleapis.com/auth/admin.directory.domain",
  "token_type": "Bearer"
}
```

The access_token is required to run individual API calls. 
In Postman, set the Authorisation to OAuth2 and pass the 
`access_token` from an environment variable e.g. 
`{{access_token}}` you can have an access_code per scope 
e.g. `{{access_token_domain}}` and `{{access_token_group}}` but 
you have to refresh each one with it's own access_code

&nbsp;  

**5) Refresh the access_code**

The access_code expires after 3599 seconds (one hour) and needs to be refreshed:

  - Export the refresh_token obtained from step (4)

  ```
  export REFRESH_TOKEN="1//03omSg5YlxYZnCgYIARAAG-you're-nuts-if-you-think-I-haven't-sanitised-this-F-flr2jVyZQ7HuJ6scO7bNzJwhKqh3f2mI_gFVqu9bQ"
  ```

  - Run the following curl command:

```
curl -s -X POST \
 -d refresh_token=$REFRESH_TOKEN \
 -d client_id=$CLIENT_ID \
 -d client_secret=$CLIENT_SECRET \
 -d redirect_uri=urn:ietf:wg:oauth:2.0:oob \
 -d grant_type=refresh_token \
 -d access_type=offline \
 -L https://accounts.google.com/o/oauth2/token
```

  - This will respond with:
```
{
  "access_token": "ya29.a0AfH6SMDEHgHzDuTDGLH9QcRW7JQzskPDmZsanatised_aumT00r36VfBYc6nxlfPLhcn-SyMAp02SwQtL6P3evjZOKkG8dsjerrJds0j0CeouOI43qxA-dkTFuSnPloGIj2nAz3tL1gVJK2HMGqM70b0",
  "expires_in": 3599,
  "scope": "https://www.googleapis.com/auth/admin.directory.domain",
  "token_type": "Bearer"
}
```

&nbsp;

## Useful Links

https://developers.google.com/google-ads/api/docs/concepts/call-structure

https://stackoverflow.com/questions/32076503/using-postman-to-access-oauth-2-0-google-apis

https://developers.google.com/oauthplayground

https://developers.google.com/people/

https://developers.google.com/identity/sign-in/web/devconsole-project

https://developers.google.com/admin-sdk


### Google API Scope 
This is space separated in Postman, but comma separated in Google:

https://www.googleapis.com/auth/admin.directory.group

https://www.googleapis.com/auth/admin.directory.domain