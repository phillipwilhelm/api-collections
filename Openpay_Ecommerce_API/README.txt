## THE OPENPAY API
Welcome to the Openpay API reference documentation. The API is based on XML and uses standard HTTP response codes. This documentation assumes you are confident with RESTful services, web programming and comfortable making http requests.



## INTRODUCTION

Openpay's ecommerce API is designed for ecommerce merchants to enable Openpay as a payment option for consumers who may elect to take out an Openpay plan.

The API facilitates the plan creation process and gives confirmation to the merchant that the plan has been successfully created, and the user is therefore entitled to have the merchant order processed.

There are three steps to the workflow:
1. The merchant provides the purchase amount and customer information to obtain a valid Plan ID.
2. The merchant forwards the customer to the Openpay "websales" website so the customer can choose their plan & receive confirmation.
3. The customer is returned back to the merchant via a callback and are notified of the outcome for instant plans. 

Nb. For pending plans, merchants request Openpay to capture the payment and receive confirmation in the response for step 3.

----



## API CALLS

The API supports the following calls. Detailed descriptions are available in the call sections below.

| Call                            | Description                                                                 |
|---------------------------------|-----------------------------------------------------------------------------|
| `NewOnlineOrder`                | Request a new plan ID.                                                      |
| `OnlineOrderStatus`             | Order status for any valid plan ID.                                         |
| `OnlineOrderPaymentStatus`      | Payment status for active plans.                                            |
| `OnlineOrderCapturePayment`     | Capture's the payment for pending plans.                                    |
| `OnlineOrderReduction`          | Refund or reduce a plan/order.                                              |
| `OnlineOrderDispatchPlan`       | Notify openpay that an order has been dispatched.                           |
| `OnlineOrderChangeDeliveryDate` | Change the delivery date of an order.                                       |
| `MinMaxPurchasePrice`           | Request the min/max purchase price configured for the merchant.             |
| `RetailerPlanInformation`       | Request plan information for the merchant.                                  |
| `OnlineOrderFraudAlert`         | Notify openpay when a customer is fraudulant after a plan has been created. |



----

## Authentication

The API uses token-based authentication namely a JamAuthToken. Tokens will be provided and must be included in the body of all requests made to the API. The JamAuthToken can authenticate any API action described in this documentation.

Jam tokens must only be used on your server, and never in the frontend of your application to avoid users obtaining the tokens and using them maliciously. 

Tokens should be shared with the minimum number of people necessary in your organisation for security reasons. Similarly, you should avoid embedding Jam tokens in your backend and instead include them in environment variables or configruations.

----



## REQUEST/RESPONSE
The API uses token-based authentication which needs to be included in the body of your request. Please ensure that all connections are using TLS 1.2

POST requests should have a Content-Type: application/xml header, except when using the `RetailerPlanInformation` call in which case use the application/json header. Responses return XML/JSON with a consistent structure.

----



## GETTING STARTED

Openpay provides a simple API which is uses HTTP response codes to indicate errors and uses only HTTP POST requests. The API is compatible with most HTTP clients and will respond with XML and JSON payloads.

To get started first obtain your test JamAuthToken from openpay which will be provided with an endpoint and your configuration details.

Once your JamAuthToken is provided you can experiment with the API calls using the Openpay postman collections herein.

Sample responses are included below for clarity.

----



## ERROR CODES

The following error codes are possible in the API responses:

| Error | Error Description                                                                     |
|-------|---------------------------------------------------------------------------------------|
| 12700 | Retailer identity key supplied not valid (check Jam Token)                               |
| 12701 | Retailer is not Active (check Jam Token)                                                                |
| 12702 | Retailer location is not Active (check Jam Token)                                                     |
| 12703 | Retailer location origin not Active (check Jam Token)                                                 |
| 12704 | Plan ID supplied does not exist                                                       |
| 12705 | Plan ID supplied is not owned by this Retailer                                      |
| 12708 | Invalid Purchase Price (<0,   Not Numeric or outside of Min/Max Purchase Price range) |
| 12709 | New Purchase Price is greater   than current Purchase Price                           |
| 12710 | New Purchase Price is less than   or equal to zero                                    |
| 12711 | Plan must be Active for this   feature to apply                                       |
| 12719 | Maximum number of requests for   Calendar Day reached                                 |
| 12721 | New Delivery Date is too close   to plan creation date.                               |
| 12722 | New Delivery Date is too far   from plan creation.                                    |
| 12723 | New Delivery Date cannot be   earlier than today.                                     |
| 12730 | Payment unsuccessful                                                                  |
| 12731 | Payment errored                                                                       |
| 12732 | Plan ID supplied is not valid   for capture                                           |
| 12733 | Plan ID has expired and may no   longer be captured                                   |
| 12734 | Plan Creation Mode unknown                                                            |