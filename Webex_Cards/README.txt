# Give new levels of interactivity to Webex Teams users with cards

Cards let you add interactivity to Webex Teams messages. Users can interact with your app in rich new ways without ever leaving the Webex Teams client.

Bots and Integrations can add cards to Webex Teams spaces by including a card attachment when posting a message. Card attachments use Microsoft's Adaptive Cards specification to define the content of the card. The Webex Teams clients render cards with the same look and feel across every platform, letting you focus on the content and the interaction without worrying about the presentation.

## Cards and Action

Cards are created by including an adaptive card attachment when posting a new message. Cards can be interactive, soliciting an action from the user, such as submitting a response to a poll; or they may be purely informational, such as displaying current weather conditions.

To make cards interactive, include actions. Actions are buttons that users can use to open a URL, show another card, or submit data from an input form within the card. Cards may include up to five actions. If you include an input form, data submitted by a user is encrypted and stored within the Webex platform. You can use webhooks to receive notifications for new form submissions. Just like other API resources that contain encrypted data, the webhook's body will not include the form submission. After you receive the webhook, you will need to retrieve the form data via the Attachment Actions API endpoint. See Handling Requests from Webex Teams in the Webhooks Guide for more information about how to use webhooks with encrypted data.

https://developer.webex.com/docs/api/guides/cards