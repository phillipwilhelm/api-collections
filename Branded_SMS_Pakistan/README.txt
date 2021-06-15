# BrandedSMS REST API

----
## Introduction

Welcome to the BrandedSMS API documentation!

Our API provides a set of flexible tools which you can use to create new outstanding projects. We smile a bit more each time we see skilled developers unleash their creativity!

## Basic API usage
All LiveChat API requests start with

    https://bsms.hostandsoft.com/app/sms/


Please note that all BrandedSMS API requests must use `HTTPS` protocol.

# API response

## Response format

By default our API respond back in JSON format but you have rights to choose in which format you would like to get the response, as we support `json` and `xml` output.

To get the desired output you may include `response=json` or `response=xml` in your API request

## Successful Responses

* 200 success
* 201 Successfully Send
* 202 SMS scheduled successfully
* 207 Subscription successfully done
* 208 Contact already subscribed
* 209 OTP Generated
* 210 Code Matched successfully.

## Error Response Code

* 401 Authentication Failed
* 101 Bad gateway requested
* 103 Invalid Phone Number
* 104 Parameters Missing
* 105 Insufficient balance
* 106 Invalid Sender id
* 107 Invalid SMS Type
* 108 SMS gateway not active
* 109 Invalid schedule time for campaign
* 110 Media URL required
* 111 SMS contain SPAM word, wait for approval
* 112 Destination number contain in blacklist number
* 113 Invalid Template Match
* 114 No Country Found
* 115 No senderid available for your account
* 116 Phone coverage not active
* 117 Subscription failed. Please try again
* 118 Subscription list not found
* 119 no groups available for your account
* 120 invalid otp provided