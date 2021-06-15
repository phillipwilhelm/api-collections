# Introduction
GLS Web API for Parcel Processing – Developer Documentation

# Overview

General Notes:

•  API Performance: 300ms - 1500ms / label.

•  Requests should be executed sequentially.

•  One request per shipment.

•  A maximum of 30 labels can be created with one request.

•  The shipment and labels are created with the same request. Since the API does not support to retrieve the label at a later time the label must be saved by the requesting application for later use. 

•  Some services return more than one label per parcel (e.g. ExchangeService returns one label, one return label and an acceptance receipt )

•  Requests with  Pick&ShipService and Pick&ReturnService do not return a label since the label will be printed in the depot.  

•  The test system creates labels that are marked with a “DEMO”-banner to make sure they are not used in production.  


# Authentication
User and Password 

# Error Codes

HTTP code  Code  Message  Description
429  0001  Rate limit exceeded  The user has exceeded the rate limit (%s).

403  0002  User account blocked  The user account was blocked. 

403  0003  Missing rights  The user is allowed to access the API, but lacks necessary rights (account registration incomplete).

400  0004  Input validation error  An error occurred when validating input: %s.
400  0005  Missing input parameter  An input parameter is missing: %s.

400  0006  Address not supported  The shipment cannot be delivered to or from a given address, details: %s.

406  0008  Not acceptable  The content-type of the POST request is not acceptable.

401  0009  Not authorized  The user is not authorized (wrong username or password).

404  0010  Page not found  The requested resource was not found.

400  0011  Parcel weight limit exceeded  A parcel weight limit was exceeded, details: %s.

405  0011  The HTTP method is not supported for this resource.  The method specified in the Request-Line is not allowed for the resource identified by the Request-URI.

500  9999  Unexpected error  There was a server-side processing failure of some kind.


# Rate limit