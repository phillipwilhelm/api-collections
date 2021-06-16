Welcome to gx-boa-ms-income-sales API!

The API is organized around REST. All request should be made over SSL. All request and response bodies, including erros, are encoded in JSON.

You could download the postman collections to test the API.

## Errors

The API returns standard HTTP success or error status codes. For errors, we will also include extra information about what went wrong encoded in the response as JSON. The various HTTP status codes we might return are listed below.

#### HTTP Status codes

| Code | Title | Description |
| -- | -- | -- |
| 200 | OK | The request was successfully. |
| 201 |	Created |	The resource was successfully created. |
| 204 |	No Content	|The request was successfully. |
| 400 |	Bad request	|Bad request |
| 404 |	Not found	|The resource does not exist. |
| 422 |	Validation error	|A validation error occurred. |
| 50X |	Internal Server Error|	An error occurred with our API. |

#### Error types

All errors are returned in the form of JSON with detail information about the type of error and its cause.

| Type | Description |
| -- | -- |
| message|	type of error |
| microservice|	Name of the microservice |
| errors |	list of errors |
| field|	name of the field causing the error |
| fieldValue|	value of the field causing the error |
| errorType|	type of error, by default "error"|
| errorMessage|	error detail message|

#### Error response example

```
{
  "message": "Unprocessable entity error",
  "microservice": "gx-boa-ms-income-sales",
  "errors": [
    {
      "field": "saleId",
      "fieldValue": "E330574E-E13B-4A3C-AE27-11FFF9F3E761",
      "errorCode": 28,
      "errorType": "error",
      "errorMessage": "Sale does not exist or is deleted"
    }
  ]
}
```

## Headers

| Header name | Description |
| -- | -- |
| Content-type	| application/json |