## Introduction

tiket.com Hotel API for B2B partner.
This document aims to provide all of the information needed for developers to use tiket.com resources, the API is for server-side or rest API

Please check F.A.Q section, it may solve some problems that you have experienced during integration and after production.

For further information, please contact our customer service

Email : [partner@tiket.com](mailto:partner@tiket.com)


#### Access to the API
In order to access our APIs, you will need an Access Token. This key is generated when you proceed with :
- **API v2** with `ID` and `MessagePassword` via **Authentication Header** and `RequestorID` and `MessagePassword` via **Authentication Body**

- **API v1** with `clientId` and `clientSecret` via **Headers**

Both will be received after successfully registering as tiket.com partners.

The tiket.com REST API is served over HTTPS. To ensure data privacy, unencrypted HTTP is not supported.
In addition, all requests are required to pass Bearer Token for authentication.
The token is predetermined and provided by tiket.com. All requests are logged and validated. All parameters must be URL-encoded.

#### Authentication 
- API v2 - <a href="#auth-v2">Refer the link</a>

B2B API v2 offers Basic Authentication using username and password or it can be pushed via body request that allows secure authorization in a simple and standard method from server to server.

- API v1 - <a href="#generate-access-token">Refer the link</a>

B2B API v1 offers OAuth2 Authentication that allows secure authorization in a simple and standard method from server to server.

#### Base URI
All URLs referenced in the documentation have the following base:
https://api.tiketsandbox.net/b2b-gateway/
