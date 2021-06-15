This reference helps you implement the RESTful Salesboard API v3. This API uses a JSON format for output and is capable of handling CORS (Cross-Origin Resource Sharing) requests. The API is stateless – all requests are validated against an PHPSESSID token. These endpoints are used by mobile, web clients and external WebServices. You can find several examples in this documentation. If you find something not working as documented please reach us on support@salesboard.biz. 


![Home](https://lh3.googleusercontent.com/pw/ACtC-3dAGSIcrVOebeMlMjFMc5NvvVBBo-nIHx5uEQSm0oCJJuqr4v7J59VZhsw_kQZBMvXOvwLOCxh4DwewkL5AYQAJIruqhbgTVkYdKewixkTVWCdi2Ws1U3Lr7kSv3cwYmrsKOLf5rRZRdJwqIZwi_fne=w2150-h1434-no?authuser=0)

### Notice!
Please be aware that any actions you perform through this reference testing functionality will involve operations with your production data. To test your applications against some sandbox data, we recommend creating a new, separate Salesboard account for sandboxing purposes. To request your own sandbox account, email us at support@salesboard.biz.

This API is under active maintenance, and we are constantly adding new functionality to this version.

### Documentation
See https://documentation.salesboard.biz for more information.

### Requirements

Each request must have

* Salesboard account (client)
* header XREQUESTEDWITH
* cookie PHPSESSID=(your-token)

### Salesboard account
Before you can start you would need to know what is the name of the Salesboard you want to target. Each account have different settings and the data is isolated, meaning that it wouldn't be possible to share login credential between different Salesboard accounts.
The domain will require these account name, set postman env variable:

            sb_client: (salesboard-account)
            https://{{sb_client}}.salesboard.biz

### Header XREQUESTEDWITH

Every request must contain the header XREQUESTEDWITH to identify the application request type.

            "XREQUESTEDWITH": "APIHttpRequest"

Possible values are:
* **APIHttpRequest** - to be used between servers for system integration and automated tasks
* **mobileHttpRequest** - to be used by the mobile app (Android and iOS)
* **WebAppRequest** - to be used by Web based applications

Please note that it is highly recommend to use the *service_account* role in combination with **APIHttpRequest**. This role will only have access to Salesboard API's. It will not be able to use Salesboard Apps neither access to the Management Area. This role is recommend for activities that are automated and do not involve human interaction.


### Access Token

For each request, a access token will be required to authenticate the user. This token can be generated using the *login* endpoint with the *username* and *password*. The returned token needs to be set as cookie for each individual request:

            "set-cookie": "PHPSESSID=(your-token>)"

### Parameters
#### Include

By default all data is returned for the each object but for some of the endpoints you will find the special parameter 'include'. This parameter allows to filter which fields to be returned for each item. In order to optimize the amount of data returned and to reduce the load on the servers you should use this parameter when available.
e.g.:

    GET https://{{sb_client}}.salesboard.biz/v1/teams/{{sb_team_id}}
    ?include=tags,contactTypes,users,managers


### Error responses

#### 400 Bad Request

The server could not understand the request due to invalid syntax.

#### 401 Unauthorized

Although the HTTP standard specifies "unauthorized", semantically this response means "unauthenticated". That is, the client must authenticate itself to get the requested response.
                
#### 403 Forbidden
The client does not have access rights to the content; that is, it is unauthorized, so the server is refusing to give the requested resource. Unlike 401, the client's identity is known to the server.

#### 404 Not Found
The server can not find the requested resource. In the browser, this means the URL is not recognized. In an API, this can also mean that the endpoint is valid but the resource itself does not exist. Servers may also send this response instead of 403 to hide the existence of a resource from an unauthorized client. This response code is probably the most famous one due to its frequent occurrence on the web.

#### 409 Conflict
This response is sent when a request conflicts with the current state of the server.

#### 410 Gone
This response is sent when the requested content has been permanently deleted from server, with no forwarding address. Clients are expected to remove their caches and links to the resource. The HTTP specification intends this status code to be used for "limited-time, promotional services". APIs should not feel compelled to indicate resources that have been deleted with this status code.

#### 429 Too Many Requests
The user has sent too many requests in a given amount of time ("rate limiting").

#### 500 Internal Server Error
The server has encountered a situation it doesn't know how to handle.