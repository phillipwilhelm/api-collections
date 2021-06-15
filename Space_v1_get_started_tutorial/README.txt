Super Cool Space Collection
===

This is a sample collection and environment for the tutorial outlined in [Not your Grandma's Postman](http://blog.getpostman.com/2017/05/27/not-your-grandmas-postman/). Read the collection documentation [here](https://documenter.getpostman.com/view/1559645/S1LvV8rH).

Retrieve the **Astronomy Pic of the Day from NASA**, get an Imgur auth token, and then post the picture to **Imgur**.

[![beautiful space pic](https://apod.nasa.gov/apod/image/1705/M101p2000bagi.jpg)](https://apod.nasa.gov/apod/image/1705/M101p2000bagi.jpg)

If you haven't already, click the Run in Postman button to get the collection and environment into your Postman app. In the Postman app, you should now see this collection in the sidebar to the left, and this environment selected in the dropdown in the top right.

[![download Space collection](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/importSpace1.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/importSpace1.png)

To get started:
===
1. **Register an Imgur app:** 

  Head to Imgur and [register a new application](https://api.imgur.com/oauth2/addclient). Select OAuth 2 authorization with a callback URL, and add the following Authorization callback URL - `https://www.getpostman.com/oauth2/callback`.
  
  Make a note of your Imgur app's `Client ID` and `Client secret`. 
  
  [![imgur client id](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurClientSecret_censored.jpg)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurClientSecret_censored.jpg) 

2. **Add your Imgur credentials to Postman:**

  In the Postman app, head to the **Quick Look** icon in the top right to view your variables. Click the **Edit** link.
  
  [![quick look icon](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurQuickLook.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurQuickLook.png)
  
  Update the `imgurClientId` and `imgurClientSecret` values with your own, and hit **Update**.

  [![update environment variable](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurEnv.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurEnv.png) 

3. **Get an auth token from Imgur:** 
  
  We will use [Imgur's OAuth 2.0 process](https://apidocs.imgur.com/#authorization-and-oauth) to get a refresh token. 

  In the Postman app, under a new request, click on the **Authorization** tab, select OAuth 2.0, click on the **Get New Access Token** button, and fill in these values:
    - Token Name: can be anything
    - Auth URL: `https://api.imgur.com/oauth2/authorize`
    - Access Token URL: `https://api.imgur.com/oauth2/token`
    - Client ID: {{imgurClientId}}
    - Client Secret: {{imgurClientSecret}}
    - Grant Type: Authorization Code
    - Request access token locally: checked
  
  [![Postman OAuth 2.0](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurAccessTokenModal.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurAccessTokenModal.png) 

  Click on **Request Token** to initiate the OAuth 2.0 flow authorizing the Postman app to connect to your Imgur account.
  
  [![Imgur Oauth](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurOauth.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurOauth.png) 
  
  Once that is completed, add the `refresh_token` value to your environment under the `imgurRefreshToken` key, the same way you added your Imgur credentials to Postman in Step 2.
   
  [![Imgur refresh token](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/refreshTokenOauth.jpg)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/refreshTokenOauth.jpg) 

4. **Run the collection:** 

  Click on the right angle bracket (**>**) next to the collection to open the collection details flyout, and click the blue **Run** button.

  [![collection details](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurRunSpaceCollection.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/imgurRunSpaceCollection.png)

  This will open the collection runner in a separate window. Verify that the correct collection and environment is selected in the respective dropdowns, and then click the **Start Run** button.

  [![collection runner](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/collection_runner2.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/collection_runner2.png)

  In the collection runner, watch your tests running (and hopefully passing). If all goes well, your picture has been posted privately to Imgur under your account.
  
  [![collection runner gif](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/collectionRunner2.gif)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/collectionRunner2.gif)