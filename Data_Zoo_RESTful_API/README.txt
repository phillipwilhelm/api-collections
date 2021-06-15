**This version of the Data Zoo API has been superceded by a new version (https://idu-api.datazoo.com/).  This version will continue to function and be supported by Data Zoo.**

*v1.20200507.15    Updated: Thursday 7th May, 2020*

Welcome to the Data Zoo IDU® RESTful API. You can use our API to access all of Data Zoo's identity verification services.

**Production:** https://rest.datazoo.com/api/

**Test:**       https://resttest.datazoo.com/api/  (all the examples in this documentation use Test)

The API is organised around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, such as HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website’s client-side code). JSON is returned by all API responses, including errors.

We have multiple language bindings available (cURL, jQuery, Ruby, Python, Node, PHP, and Go). You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

The following assumptions have been made and should be considered when submiting a request via this API:
* Only authorised users who have been issued an User Name and Password can access this service
* The authorised users understand their obligations and are familiar with, and have agreed to the [Data Zoo Privacy Policy and Terms & Conditions][link] as displayed on the website.

  [link]: https://www.datazoo.com/privacy-policy/

**To return to the Data Zoo website, please click [here][mainsite].**

  [mainsite]: https://www.datazoo.com/
  
# Questions/Comments/Suggestions #
If you have any questions or comments, please let us know via our [Support Portal][support].  Alternatively, please search our [Knowledge Base][knowledge] for answers to FAQ's and other general advice.

  [support]: https://datazoo.freshdesk.com/support/tickets/new
  [knowledge]: https://datazoo.freshdesk.com/support/home
  
# Terms of Access #
## Consent ##
There are available data sources that will require consent and can only be accessed where the individual who an enquiry is being made on has consented for the enquiry to be performed.  This consent, either in written or electronic form, is to be stored by you as proof that consent has been obtained and if required could be made available to Data Zoo for audit purposes.

## Data Sources ##
The data sources provided to you are as provided to Data Zoo from its’ suppliers.  No warranty is provided by Data Zoo for the accuracy of the data, or in the transmission or matching of the data through the API service.

# Errors #
## System Errors ##
| Error         | Description   | 
| ------------- |:-------------:| 
| 200 - OK      | The request was successful. If you are getting unexpected results, please check any Status or Error messages that have been returned in the response. If you believe there may be a problem, please raise a ticket with our Support team at https://datazoo.freshdesk.com/support/tickets/new.|
| 400 - Bad Request | The request could not be understood by the server. Please ensure the request is in the appropriate format and all necessary headers have been included.      | 
| 403 - Forbidden  | The request was valid, but the requestor does not have appropriate permissions. Please ensure your username is correct and your access token is still valid. If your access token has expired, you may need to reauthenticate your credentials to get a new token.            |
| 415 - Unsupported Media Type | The request entity has a media type which the server or resource does not support. For example, the client uploads an image as image/svg+xml, but the server requires that images use a different format.|
| 500 - Internal Server Error | There was a back-end error when processing the request. Please ensure your request is in the correct format and retry. If you receive this error again, please raise a ticket with our Support team at https://datazoo.freshdesk.com/support/tickets/new.|
| 522 - Origin Connection Time-out | There was a back-end error when processing the request. Please resubmit the request. If you receive this error again, please raise a ticket with our Support team at https://datazoo.freshdesk.com/support/tickets/new.|

## Data Source Errors ##
For a complete list of our Data Source errors please refer to the "Status & Data Source Errors" table at the bottom of this page.