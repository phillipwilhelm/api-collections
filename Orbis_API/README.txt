# Overview
-----------

The goal is to provide third party developers with a way to connect their proprietary system with a fully functional trading platform thus allowing clients with a secondary point of entry to their accounts. The document is aimed at developers who are familiar with the technology mentioned in the document.
API is written so as to provide a simplified and unified singular point of access to the system. As new requirements come to light, the system will change as necessary. This may mean drastic changes to the core functionalities such as authentication, requests or responses. Keep in mind, new fields are added at will therefore client system must support changes without breakage.

# Overall guidelines
---------------------

### Domain

API domain for requests will be provided during initial set up.

### URI

Subject to change in future. Currently all API requests are routed via: `/api/`

### Scheme

All requests must be made in secure manner via SSL. For UAT environment, if one provided, server certificate may be expired or for a different domain.

### Request/Response

All requests are made via `GET` or `POST` via `HTTP/1.0` or `HTTP/1.1` protocol. `GET` requests have specific URI patterns with given extra parameters for desired data output as described below. All responses are JSON formatted in `UTF-8` encoding. Unless otherwise noted, all requests should be made via `GET`.

If there's an error processing the request, an error response will be returned. Error response is indicated by 500 response code and the body will include `JSON` object as described below. Each error will have a unique `id` assigned to it. It is recommended to retain that ID for reference.

`{timestamp: 'MM/dd/yyyy HH:mm:ss z', error: 'Not permissioned', id: '123456789'}`

|Response   |                           |
|-----------|----------------------------------------------------|
|*error*    |Textual representation of the error where available.|
|*errors*	|Array of multiple errors.							 |
|*timestamp*|Server timestamp. Format: `MM/dd/yyyy HH:mm:ss z`	 |
|*id*   	|Unique ID for the error.							 |

# Authentication
----------------

Authentication mechanism is to be provided in a separate document.