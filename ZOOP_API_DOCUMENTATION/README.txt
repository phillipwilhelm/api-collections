## Getting Started

The Zoop APIs are organized around REST. All calls to the Zoop API should be made to `https://prod.aadhaarapi.com` for now, We will slowly migrate to Zoop.one base URL. All responses are formatted in JSON. 

You can view code examples in the dark area to the right. You can switch the programming language of the examples using the tabs above.

## Enabling API access

To begin using the zoop API, you will need to enable the API and generate an API key. This can be done by logging into the [dashboard](https://dashboard.aadhaarapi.com/) and visiting  API Keys.


## Authentication


| Headers Parameter | Headers Value |
| -------- | -------- | 
| qt_api_key     | {Your Key}    | 
| qt_agency_id     | {Your Agency ID}    | 
| Content-Type| application/json     | 


Most calls will require authentication. Zoop supports HTTP authentication. You will need to pass through your secret API key.

NOTE: For IP Whitelisting, please contact your Account Manager or open a [ticket](https://aadhaarapi.freshdesk.com/)  

Security note: All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail. 

## Environment URL(Base URL)

1. Production URL: `https://prod.aadhaarapi.com` 
2. Staging URL: `https://preprod.aadhaarapi.com` 


## ZOOP SDK AND DOCUMENTATION 
> For E-Sign, Bank Statement Analysis, and Offline Aadhaar 

1. [ZOOP ANDROID GATEWAY SDK](https://github.com/zoop/zoop-gateway-android-sdk) 
2. [ZOOP WEB GATEWAY SDK](https://github.com/zoop/zoop-web-sdk)
3. [ZOOP OFFLINE AADHAAR SDK](https://github.com/zoop/zoop-offline-aadhaar-android-sdk)