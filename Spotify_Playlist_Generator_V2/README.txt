Blog series:
* [Conditional workflows in Postman](https://blog.getpostman.com/2016/03/23/conditional-workflows-in-postman/)
* [Generate spotify playlists using a Postman collection](https://blog.getpostman.com/2016/11/09/generate-spotify-playlists-using-a-postman-collection/)
* [Daily mix with Postman monitors and spotify](https://blog.getpostman.com/2017/03/28/daily-mix-with-postman-monitors-and-spotify/)

<a href="https://docs.google.com/drawings/d/11GIo2IAQmictmFJuxIJ3sj1zi_nFSDlm_uJMLa9I3WE/pub?w=1410&amp;h=772" target="_blank"><img src="https://docs.google.com/drawings/d/11GIo2IAQmictmFJuxIJ3sj1zi_nFSDlm_uJMLa9I3WE/pub?w=1410&amp;h=772"></a>

The Spotify playlist generator collection lets you get your daily/weekly dose of fresh music. Modeled on the AMAZING [Spotify Discover Weekly](https://www.spotify.com/discoverweekly/), within 5 minutes you'll be able to set this up, and even tweak it to your heart's content!

### Workflow

<a href="https://docs.google.com/drawings/d/1p7imXUIWIC9t5vX4B5jD2XuY6MoYOYcT9I9gJVi87ic/pub?w=1532&amp;h=241" target="_blank">
<img src="https://docs.google.com/drawings/d/1p7imXUIWIC9t5vX4B5jD2XuY6MoYOYcT9I9gJVi87ic/pub?w=1532&amp;h=241"></a>

1. Take a list of artists as input
2. Randomly select an artist from this list and usse Spotify's fantastic [Get Related Artists](https://developer.spotify.com/web-api/console/get-artist-related-artists/) and [Get an Artist's top tracks](https://developer.spotify.com/web-api/console/get-artist-top-tracks/) APIs to mashup a playlist
3. Add these related artists back to the original list and persist back to the environment

### Setup the Environment

Click on the Run in Postman button above to import the collection and environment template within your app.

1. ##### Spotify
    * Head to [Spotify Developer](https://developer.spotify.com) and register, then create a new app in the My Applications section. Add the `client_id` and `client_secret` to your environment.
    * Under the newly created app config, add the following Redirect URI - `https://www.getpostman.com/oauth2/callback`
    * We'll use the [Authorization Code Flow](https://developer.spotify.com/web-api/authorization-guide/#authorization-code-flow) to obtain the Refresh Token.
    * Open Postman, under a new request, click on the Authorization tab, select OAuth 2.0 and fill in these values:
    - Token Name: can be anything
      - Auth URL: https://accounts.spotify.com/authorize
      - Access Token URL: https://accounts.spotify.com/api/token
      - Client ID: {{client_id}}
      - Client Secret: {{client_secret}}
      - [Scope](https://developer.spotify.com/web-api/authorization-guide/#scopes): `playlist-read-private playlist-modify-private`
      - Grant Type: Authorization Code
      - Request access token locally: Checked
  * Click on Request Token, go through the OAuth flow, and add the `refresh_token` to your environment
     
2. ##### Postman Cloud API
    * Generate a Cloud API key [here](https://app.getpostman.com/dashboard/integrations)
    * Store this value under `postman_api_key`
    * (Optional) For a smarter generation, we'll want to the environment to update as well. Get the newly created environment id using the Cloud API as outlined [here](https://api.getpostman.com/#dbd079-e3e1-aa08-7e21-66f55df99351). In your environment, set the `environment_id` value to the uid obtained above

3. ##### Collection Config
  Set the following variables in your environment
  * `user_id`: your spotify username
  * `country_code`:  in [ISO 3166-1](http://en.wikipedia.org/wiki/ISO3166-1alpha-2) format
  * `N`: defaults to 5. Refer to the algorithm section for more details
  * `artists`: List of seed artists for the collection. You can find them as part of the Spotify artist link (Available in the app): e.g. for Oasis, the link looks something like https://open.spotify.com/artist/2DaxqgrOhkeH0fpeiQq2f4, choose the last section. The artists variable is an array of strings, so it'll look something like: ["2DaxqgrOhkeH0fpeiQq2f4", "2ooIqOf4X2uz4mMptXCtie"]

### Run and Schedule the Collection

1. To verify that everything works as expected, run the collection in the Postman app using the [Collection Runner](https://www.getpostman.com/docs/running_collections)
2. Now you can use [Postman Monitors](https://monitor.getpostman.com/) to schedule the collection run daily or monthly. 
  
<a href="https://docs.google.com/drawings/d/1urC-cLZXeE7ot59jOptURcHMCX4oeRAiUTFzADAU9wQ/pub?w=1437&amp;h=839" target="_blank"><img src="https://docs.google.com/drawings/d/1urC-cLZXeE7ot59jOptURcHMCX4oeRAiUTFzADAU9wQ/pub?w=1437&amp;h=839"></a>