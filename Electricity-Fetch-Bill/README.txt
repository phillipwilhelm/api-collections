Electricity is one of the crucial things in our lives not only for households but for large industries as well. Paying electricity bill on time is very important to avoid disrupted services. paythrough.in provides you with the easiest and fastest method to know and pay your electricity bill. Just a few taps and your electricity bill payment is done. **Electricity-Fetch-Bill** process requires the following headers
* SANDBOX-API-KEY
* SANDBOX-PRODUCT-KEY
* MERCHANT-CODE
* SERVICE-CODE
# REQUEST NUMBER
# VENDOR
# API METHOD
# EXTRAPARAM
# BASIC
This API service is used to fetch the electricity bill.

URL:-{{base-url}}/electricity-payment
## ELECTRICITY FETCH BILL STATUS

Status | Description
------------ | -------------
204 | Failure
200 | Success


**POST** VERIFICATION API\
`{{base-url}}/electricity-fetch-bill`
## REQUEST JSON
### BODY PARAMS
* Request Number required:-Request Number needs to be verified.
* Vendor required:-Vendor needs to be verified.
* API Method required:-API Method needs to be verified.
* Extra Param required:-EXTRA PARAM needs to be verified
## OUTPUT

### INVALID REQUEST NUMBER 
```css

{
  "responseCode": "204",
  "responseMessage": "Please provide a Request Number."
}


```


### INVALID VENDOR
```css

{
  "responseCode": "204",
  "responseMessage": "Please provide the Vendor Name."
}


```


### INVALID API METHOD
```css
{
  "responseCode": "204",
  "responseMessage": "Please provide a Method."
}


```

### INVALID REQUEST
```css
{
  "responseCode": "405",
  "responseMessage": "GET METHOD NOT ALLOWED"
}


```

### Electricity-Fetch-Bill successful
```css
{
  "responseCode": "200",
  "responseMessage": "success",
  "billFetchPrice": "10000"
}
```
###### SANDBOX-API-KEY
J2CMd8V2VvQtYM72ch
###### SANDBOX-PRODUCT-KEY
{{Product_key_value}}
###### MERCHANT-CODE
{{Merchant-Code value}}
###### SERVICE-CODE
{{Service-Code value}}

BODY raw
```css
 {
    "RequestNumber":"<<Request Number>>",
    "vendor":"<<vendor>>",
    "apiMethod":"<<api Method>>",
    "extraParam":"<<extra Param>>"
}
```
Example Request\
`Verification API`
```css
 curl--location--request POST '{{base_url}}/electricity-fetch-bill'\
 --header 'SANDBOX-API-KEY:J2CMd8V2VvQtYM72ch' \
 --header 'SANDBOX-PRODUCT-KEY:{{SANDBOX-PRODUCT-KEY_value}}' \
 --header 'MERCHANT-CODE:{{MERCHANT-CODE}}' \
  --header 'SERVICE-CODE:{{SERVICE-CODE}}' \
 --data-raw '{
          
				   
		    "RequestNumber":"<<Request Number>>",
		    "vendor":"<<vendor>>",
		    "apiMethod":"<<api Method>>",
		    "extraParam":"<<extra Param>>"
		    		
}'


```