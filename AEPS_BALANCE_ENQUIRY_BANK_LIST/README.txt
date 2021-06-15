Aadhaar Enabled Payment System (AEPS) is a type of payment system that is based on the Unique Identification Number and allows Aadhaar card holders to seamlessly make financial transactions through Aadhaar-based authentication. The AEPS system aims to empower all sections of the society by making financial and banking services available to all through Aadhaar.
**AEPS BALANCE ENQUIRY BANK LIST** requires the following headers
* SANDBOX-API-KEY
* SANDBOX-PRODUCT-KEY
* MERCHANT-CODE
* SERVICE-CODE
# BASIC
This is an API based service which allows you to get AEPS balance enquiry bank list.\
URL-{{base-url}}/aeps-bank-list
## AEPS BALANCE ENQUIRY BANK LIST STATUS

Status | Description
------------ | -------------
204 | Failure
200 | Success

## Response Codes
Status Code | Description
------------| -------------
204  | Header Params Error
423  | SANDBOX API ERROR
405  | GET METHOD NOT ALLOWED
402  | Wrong number of segments
401  | Only One user allowed
423  | This service is under maintenance mode



**POST** VERIFICATION API\
`{{base-url}}/aeps bank-list`
### Response Type
JSON Object Request
### Invalid Request
```css
{
  "responseCode": "405",
  "responseMessage": "GET METHOD NOT ALLOWED"
}
```
### Invalid Header Parameter
```css
{
  "responseCode": "204",
  "responseMessage": "Header Params Error"
}
```
### AEPS BANK LIST WITHDRAW SUCCESSFUL
```css
{
    "responseCode": "200",
    "responseMessage": "success",
    "JWTTOKEN": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eylkIjoiUEFZMTAwMDAwNCIsI",
    "bankList": [
        {
            "bank_iin": "607153",
            "bank_name": "Axis Bank"
        },
        {
            "bank_iin": "607161",
            "bank_name": "Union Bank Of India"
        },
        {
            "bank_iin": "607387",
            "bank_name": "Bank of Maharashtra"
        },
        {
            "bank_iin": "607085",
            "bank_name": "Oriental Bank of Commerce"
        },
        {
            "bank_iin": "607152",
            "bank_name": "HDFC Bank"
        },
        {
            "bank_iin": "508534",
            "bank_name": "ICICI bank"
        },
        {
            "bank_iin": "607396",
            "bank_name": "Canara Bank"
        },
        {
            "bank_iin": "607075",
            "bank_name": "Vijaya Bank"
```

###### SANDBOX-API-KEY
API-KEY Value
###### SANDBOX-PRODUCT-KEY
PRODUCT-KEY Value
###### MERCHANT-CODE
MERCHANT-CODE Value
###### SERVICE-CODE
SRV0025

Example Request\
`Verification API`
```css
 curl--location--request POST '{{base_url}}/aeps bank-list'\
 --header 'SANDBOX-API-KEY:{{API-KEY value}}' \
 --header 'SANDBOX-PRODUCT-KEY:{{PRODUCT-KEY value}}' \
  --header 'MERCHANT-CODE:{{MERCHANT-CODE value}}' \
 --header 'SERVICE-CODE:SRV0025' \
 --data-raw '{
             "none"
    
}'


```