 
![image](https://i.imgur.com/ZZN7pFW.png)

## Introduction

Welcome to JobProgress API.

JobProgress API is a powerful way to communicate with JobProgress resources. JobProgress' API exposes endpoints to communicate with JobProgress using the programming language of your choice. JobProgress API is a RESTful API based on HTTP requests and JSON responses.

This version of the API, version 3.0, uses OAuth 2.0. This means that all requests need to be encrypted and sent via HTTPS and to call any API endpoint, an access token is required. The API access token can be generated from the JobProgress dashboard.  

API Base URL
============

##### Base URL

`https://api.jobprogress.com/api/v3`

> Full URL to  get the list of all customers
> https://api.jobprogress.com/api/v3/customers


Authentication
=================

You'll need an access token to interact with the JobProgress API. To get your access token, log in to your JobProgress account and visit Settings -> Developer page.
If you are already logged in then [click here](https://www.jobprogress.com/app/#/developers) to generate an access token.

Note: As of now only admin users are able to generate the access tokens. So if you don't have an admin account please contact your admin.

Make sure to pass the access token in the below format when you make a request to JobProgress API.


`Authorization: Bearer YOUR_ACCESS_TOKEN`



Includes[]
======================

Most of our GET APIs support a way to demand additional data along with the primary Resource. You can specify that by sending an `includes[]` param with the request.

For example, if you get a list of jobs then you can send `address` and `customer` in the includes to have them added to the response. Your request will look like below:

Example: `/jobs?includes[]=address&includes[]=job`

A list of valid include values is provided in the individual sections of the API endpoints.



Data Limit 
=========

In the listing endpoints like Jobs listing number of items to be returned is limited to 10 by default. It can be changed with the `limit` parameter and the limit can be up 100 items per request.

Example: `/jobs?limit=20`


Errors
======

The API makes use of the standard HTTP codes to communicate the response type. The following are the most commonly returned status codes.

Error Code | Meaning
---------- | -------
200 | Success Response  -- Your HTTP request is successful.
413 | Bad Request -- Your request data is invalid.
401 | Unauthorized -- Your API key is wrong or API key is missing.
403 | Forbidden -- The resource requested is hidden for administrators only.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access a resource with an invalid method.
429 | Too Many Requests -- You're requesting too much! Slow down!
500 | Internal Server Error -- Something went wrong while processing the request. You can either try again or you can contact us for support.
503 | Service Unavailable -- We're temporarily offline for maintenance.


Need help?
==========

The JobProgress team is always around answering questions. The quickest way to reach us is via email support@jobprogress.com

