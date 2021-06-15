# How do I use Postman with Smartcar?

# What is Postman?

Postman is a collaboration platform for API development. Postman's features simplify each step of building an API and streamline collaboration so you can create better APIs—faster.

You’ll need a few things to start making API calls with Smartcar and Postman:

- [A Postman Account](https://identity.getpostman.com/signup?continue=https%3A%2F%2Fgo.postman.co%2Fbuild)
- [A Smartcar account](https://dashboard.smartcar.com/signup)
- [Smartcar’s Postman Collection](https://www.getpostman.com/collections/314384a97766ce52da47)

# Using **Smartcar's Postman Collection**

### Smartcar Account

If you haven’t already signed up for a Smartcar account, you can do so from this [signup link](https://dashboard.smartcar.com/signup).

Grab your Client ID and Client Secret  when you sign in, and copy them to someplace secure. You’ll need those tokens a little later in this setup.

### Configuring Postman for the Access Token

Make sure you've set up your [Smartcar Developer Account](https://dashboard.smartcar.com/) and have added the following to your application's Redirect URIs on your Smartcar dashboard. This will ensure that Smartcar Connect completed successfully with both Postman's Native and Web clients.

- `https://oauth.pstmn.io/v1/browser-callback`
- `http://localhost:8000/exchange`


Select the "Smartcar API" collection

Now you'll need to fill in a few fields to successfully make your way through the Smartcar Connect Flow. Under "**Configure New Token**"

- **Client ID:** Retrieve from your Smartcar Dashboard
- **Client Secret:** Retrieve from your Smartcar Dashboard

This collection uses Smartcar's **Test Mode** which allows you to simulate authorization and receive random values from our API. If you'd like to test with a live vehicle drop the `mode=test` parameter from the **Auth URL** in the Authorization configuration above. If you're outside the US and want to use a live vehicle follow [this guide](https://www.notion.so/Passing-the-Country-Feature-Flag-d7d1e6ded23e4fc4b873c4a154a88766).


Next hit  **Get New Access Token**. You'll be prompted to walk the through the Smartcar Connect Flow. 


Hit **Use Token**. You should see **Access Token** under **Current Token** Populate with the  access token from the popup.

Using this access token you can make requests to Smartcar's API.

This access token is only valid for two hours. If you want to make API requests after the fact, you'll need to generate a fresh acces token by stepping through the Connect Flow as outlined above or get a new one using our [Refresh Token Exchange](https://smartcar.com/docs/api#refresh-token-exchange).

# **Making a request to the API**

Thanks to Postman, the requests in the collection will inherit the `access_token` form the OAuth 2.0 Authorization we went through in the steps above. 

The first thing you'll want to do is get a **vehicle ID** from the `All Vehicles` request. By default, if you authorized more than one car in Smartcar Connect, this collection will take the first ID from the list and assign is to the [collection variable](https://learning.postman.com/docs/sending-requests/variables/#variable-scopes) `vehicle_id`.

If you want to get info from another car, feel free to to overwrite the collection variable `vehicle_id` with the ID you want from the `vehicles` list

Now that you've got a vehicle ID, you can make a request to one of our endpoints.

If you're getting a `403 - permission_error`, you'll want to make sure that the car you've set as the vehicle ID is compatible with the endpoint. For example a 2016 Audi A4 isn't an EV so you won't be able to check it's EV Battery Level.