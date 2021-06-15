## Installation

1. Install Postman 7.18+

2. Download and import [collection file](https://raw.githubusercontent.com/cardpay/postman-sdk-v3/master/collection.json)

3. Download and import [environment file](https://raw.githubusercontent.com/cardpay/postman-sdk-v3/master/sandbox.json)


## API usage

Execute any section from Postman collection.  
For more information about API v3 please visit [documentation web-site](https://integration.unlimint.com).


## Notes

* constants ('UNLIMINT_API_URL', 'PAYMENTPAGE_TERMINAL_CODE' and so on) are [Postman environment variables](https://learning.postman.com/docs/postman/variables-and-environments/variables/), defined for 'sandbox' environment.
* following variables are defined for collection scope *(click 'Edit' button on 'unlimint-api' collection and see 'Pre-request Script' section)*:
    * request_name &mdash; name of the test that is being executed, using for 'merchant_order.description' field value, in request's 'Body' section
    * expiration &mdash; customer's card expiration date, using for 'card_account.card.expiration' field value, in gateway request 'Body' section. Format: mm/yyyy
    * tokens &mdash; variable with 'obtain' function which is calling in order to get API authorization tokens
* other variables ('{{payment_id_to_complete}}', '{{payment_id_to_reverse}}', etc) are defined in 'Pre-request Script' and 'Tests' sections for particular request.