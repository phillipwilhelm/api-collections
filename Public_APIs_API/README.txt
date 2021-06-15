Public APIs github repo (https://github.com/public-apis/public-apis) is a collective list of free APIs for use in software and web development. This is hosted at https://public-apis-api.herokuapp.com/. All responses are sent over HTTPS.

## Rate limiting
All requests to the above hosts are limited to 10 requests / minute. You can get status of your current limit by checking the response headers.

## Authentication
The server supports only Token Authentication. Each token has expiration time of 5 minutes. Once a token expires you can request for a new token.

After getting the token all requests have to be added with `Authorization: Bearer {{token}}` header.