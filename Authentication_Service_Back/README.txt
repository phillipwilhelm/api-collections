## Introduction
This service handles the authentication of user credentials when
attempting to access the Riskalyze network. This includes both advisors
logging in to the product as well as third-party APIs integrating with our system.

## Error Codes
| Code       | Description
|:----------:| -------------------
| **4xxxxx** | **Client-Side Errors**
| 400000     | Generic client-side error
| 400100     | Resource Not Found
| 400200     | Validation Error
| 400300     | Authentication Failed
| 400400     | Resource Conflict
| **5xxxxx** | **Server-Side Errors**
| 500000     | Unexpected server-side error

##Authorization

Certain endpoints require an Authortization header 

```Authorization:Key {{apiKey}}```

In order to obtain a new api key please PR one into the repository and request an data change in production.