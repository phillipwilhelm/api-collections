This Postman collection showcases the various OODAPI endpoints, and example usages of them. 

# **Important Notice**

**Any updates or actions performed by these requests do impact the server on which they run.** If you update, add, or delete information -- it will be updated, added, or deleted on the targeted server on a successful request.

Please make sure your `CompanyID` is set to a test company for testing, otherwise some actions on REST endpoints will default an empty `CompanyID` to the one you have current access to, and may alter live production data!

## Getting Started

**Variables**

You will see variables set with placeholder text within double curly braces, in both the URL and the body section of GET and POST requests respectively. This is the formatting for string interpolation, which will replace the double curly braces as well as the placeholder text for the variable with the current value established in the `Variables` tab of the `OODAPI Examples` collection.

This Postman collection makes use of two variables -- `APIKey` and `ServerPath`. You only need to update these two variables in order to change **all** requests in this collection. This makes it much easier to modify the `APIKey` and server you're testing on.

**Recommended Setup**

The OODAPI generally requires the `API Key` to be provided in the form of an `HTTP Header` with `X-API-Key` or in the `body` of the `HTTP Request`, typically in `JSON` format. (`XML` is also supported, though discouraged.)

***You must have the following:***

1.  A valid API Key. You can get this from the `Users` master screen within the `Odyssey Web Interface`.
2.  Update the `APIKey` variable in this Postman collection with the API Key you get from Odyssey.
3.  Update the `ServerPath` variable in this Postman collection with the location of your `OODAPI`.  

For **B&L Cloud customers**, your `OODAPI` URL exists at `https://api.blinfo.com/<name>`  
For **On Premise customers**, your `OODAPI` URL exists at the location of your Odyssey install, with `OODAPI` appended. For example, if you go to `https://mydomain.com/odyssey/odyssey.aspx` to get to the Web UI, your `OODAPI` would exist at `https://mydomain.com/odyssey/OODAPI`

## Support

Please contact B&L Information Systems for additional support.