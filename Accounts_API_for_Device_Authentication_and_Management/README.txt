The BYUB Accounts Service uses the [GraphQL](https://graphql.org/) query language for it's API.

Some examples in this documentation have more than one example, which can be viewed on the right side of the screen by clicking the drop-down box under `Example Request`.

Additional documentation is available in [confluence](https://byub-kb.byu.edu/display/SER/Device+Registration+Documentation).

This page documents the API calls required to login on a device without the need to enter a username and password. This is accomplished by doing the following steps:

1. The device makes a pre-registration call. The response returns an object with a registration token, which is displayed to the user.
2. The device begins polling the server with a series of `link device` requests. This continues in the background while the user completes the registration process in a web browser.
3. The user logs into their BYUtv account and navigates to `https://byutv.org/register`. They enter the registration code (provided in step 1) into the website. The device should now be linked to the user's account. **Note**: The website is still under development and may not work, but it is still possible to complete this step by calling the API directly via the `register device` query.
4. At this point, the device should still be polling the server with `link device` requests. After step 3, a `link device` response will indicate that the registration process is complete and provide an access token and refresh token.