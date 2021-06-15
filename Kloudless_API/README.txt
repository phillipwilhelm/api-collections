
Thank you for checking out the Kloudless Postman collection!

Kloudless is a unified API platform that enables you to quickly integrate with
several cloud services with a single implementation.

This collection contains endpoints that allow you to interact with a myriad of
different cloud storage services (Storage endpoints), as well as endpoints
utilized in managing the Kloudless application and its users (Core endpoints).

This collection works in conjunction with Postman's environment variables
to help facilitate usage. The first method requires you to go through the OAuth
2.0 flow via the Kloudless API Explorer, and copying the generated token
into the Postman environment variables. The second method utilizes Postman's
built-in OAuth 2.0 implementation. This may be helpful if you are familiar with
Postman collections, and also allows you to generate new Bearer Tokens without
navigating to the Kloudless website.

To get started, you will need a Kloudless account. If
you don't have one, you can [sign up for one
here](https://developers.kloudless.com/account/signup). If you already have an
account, you can [log in](https://developers.kloudless.com/account/login) to get
started.

To use Kloudless's API Explorer to generate a Bearer Token, navigate to [the API
Explorer](https://developers.kloudless.com/api-explorer/), and connect an
account to your Kloudless app. This will supply you with a Bearer Token. Copy
and paste this value into the Kloudless environment, as the 'Current Value' for
the `{{accessToken}}` variable. Now any API request made from the Postman
application will include the Bearer Token.

The second method will require you to navigate to the Authorization tab for the
Kloudless collection. Right click on the collection, select 'Edit', and then
select the Authorization tab. You should see a section that looks like this:

---
![OAuth set-up part 1](https://kloudless.com/wp-content/uploads/2019/02/auth-1.png)
---

Click on the Orange 'Get New Access Token' button. You will see a small form
asking for several pieces of information. It should look something like this:

---
![OAuth set-up part 2](https://kloudless.com/wp-content/uploads/2019/02/oauth2.png)
---

Here is a breakdown of what you will need to enter on the form:

* **Token Name** - The name you choose does not have an impact on the token's
viability, choose whatever name you see fit. Keep in mind, you will be able to
generate and save many different tokens so descriptive names can be useful.
* **Grant Type** - Select 'Implicit'.
* **Callback URL** - This must be a valid URL format. You will also need to add
this to the list of registered Redirect URIs for your Kloudless application. You
can add that on the [Details page for your Kloudless
App](https://developers.kloudless.com/applications/*/details). Note: You can use the depicted URL in your app, just be sure to add it to both the Postman collection and the Kloudless application's list of redirect URIs.
* **Auth URL** - Add the Kloudless OAuth URL,
`https://api.kloudless.com/v1/oauth`.
* **Client ID** - Use the Kloudless App ID for this value. This can also be found
on the [Details page for your Kloudless
App](https://developers.kloudless.com/applications/*/details).
* **Scope** - Setting this to `any:all.all` will prompt the user to select the
cloud service to authenticate. You can this to just the services you need by
setting the scope as defined on our documentation of the [Oauth
flow](https://developers.kloudless.com/docs/v1/authentication#oauth-2.0-first-leg).
* **State** - You can set this value yourself, however Postman has some built in
dynamic variables that can assign a random integer here, `{{$randomInt}}`.
* **Client Authentication** - Select 'Use as Basic Header'.

Once you have added the required information

That's it! Any API requests you now make via the Postman collection will
automatically use this value to authorize access. If this is your first time
using Kloudless, there is a small collection of API calls to quickly walk
through some basic functionality.
