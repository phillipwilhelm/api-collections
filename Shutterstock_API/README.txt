# Getting Started

The Shutterstock API provides access to Shutterstock's library of media, as well as information about customers' accounts and the contributors that provide the media. It allows customer platforms to search for media, view information and previews for the media, and license and download media.

1. Create an application at [https://www.shutterstock.com/account/developers/apps](https://www.shutterstock.com/account/developers/apps). To license media, you also need a paid subscription, but the API provides a free option for you to try out the API without licensing media. For information about applications and subscriptions, see [Subscriptions](https://api-reference.shutterstock.com/#subscriptions) in the API reference.
1. Authenticate to the API to get a token. You can get a token from the application page, or you can use the methods described in [Authentication](https://api-reference.shutterstock.com/#authentication) in the API reference.

Now you're ready to make your first API request.

## Basic API requests

Let's search Shutterstock's catalog of images:

1. In the Postman **Collections** tab, open the Shutterstock API collection dropdown.
1. In the collection, click **Images** > **Search** > **Search for images**. This request uses the API `GET /v2/images/search` endpoint.
1. Click the **Authorization** tab of the request.
1. In the **Type** dropdown, select **OAuth 2.0**.
1. Enter your Shutterstock access token in the **Access Token** box.
1. Click the **Params** tab of the request.
1. In the `query` parameter, type a search term, such as "flowers."
1. Click **Send**.

The API response contains 20 images, including URLs to thumbnails. To customize your search, check out the full list of parameters on the `GET /v2/images/search` endpoint.

## Other resources

For full documentation, check out our [api-reference](https://api-reference.shutterstock.com/#overview).

To learn more about all of the services that we offer to developers, head over to our [developer portal](https://www.shutterstock.com/developers).


---------------------------------------------------------------------------------