The Field Boundary API allows you to access and control data stored in your account with ease.

# Overview

1. You need a valid `API Token` to send requests to the API endpoints. To get a valid API Token, please send a request from here [https://www.field-boundary.com/trial-api-key](https://www.field-boundary.com/trial-api-key). After 		   receiving the API Token, you will be able to:
	
	* detect a single field boundary.
	* detect multiple field boundaries within an area.
	* retrieve the timestamp of a field boundary.
	* check your account information (e.g. number of requests).
	  
2. Response to every request is sent in [JSON format]. If the API fails to process your request, it will throw an error message within the JSON response.
	
3. The API calls will respond with appropriate [HTTP status codes] for all requests. When a response is received, a status code will be returned with its description.
	

# Authentication

To use any of the Field Boundary's APIs, you'll need the API access token (see the [Overview](#overview) section to read how to request one). Every request must contain a valid token that can be either inserted in token query parameter or provided in the form of an `Authorization` request header. In your implementation, please follow this documentation of each request header.


## API Token-related error response

If an API Token is missing, misspelt or invalid, you will receive a `403 Forbidden` or `401 Unauthorized` response code and the following JSON response:
	
```
{
    "detail": "Authentication credentials were not provided."
}
```


# Custom rate limit

The Field Boundary API has a custom rate limit that corresponds to the number of requests your account has available. Each endpoint has its own custom rate limit. Notice that such custom rate limit is not associated to the rate limits of the REST API.