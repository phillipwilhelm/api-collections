Ready to start using our API? 
Head over to the [Getting Started](#getting-started) section.

---

Getting Started
===============

To get started, you need the following things:

1.  An account - [Sign up here](https://comanage.me/en/signup)
2.  An API token - [More info](#authentication)

Note: For some API calls you'll need a [paid subscription](https://app.comanage.me/team/billing).

---

Authentication
==============

The CoManage API uses API keys to authenticate requests. You can view and manage your API keys in the [CoManage settings](https://app.comanage.me/settings/general/integrations).

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.

To make an authenticated API request, you must set your API key as a bearer token for the authentication header, like so: `"Authorization: Bearer {your_api_key}"`

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.