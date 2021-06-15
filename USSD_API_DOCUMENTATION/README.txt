# INTRODUCTION

When you dial ****920#*** on your mobile phone, you will definitely be using a USSD (Unstructured Supplementary Service Data) application.

USSD allows the transport of small data volumes over the signaling channel. It does not need an active data connection nor does it incur SMS costs. Processing USSD requests using our API is very fluid once your account is set up.

Our USSD API allows developers to create their own menu structure with the use of HTTP/S.

### Why Use a USSD?

- It is accessible on all cellular networks and mobile handsets
- WAP browsing, prepaid callback service
- Mobile money services
- Location-based content services
- Menu-based information services (Balance Enquiry, etc)
- Serves as a part of configuring the phone on the network.


# PREREQUISITE

To successfully complete the integration the following details are required as described in table 1.0 below:
---

Table 1.0

REQUIREMENT       | DESCRIPTION
---------------   | -----------------------
USer ID           | This is a unique identification created by Nalo for third parties doing the integration
Endpoint URL      | This is the URL where all requests from the mobile handset will be terminated. This should be provided by the other part to NALO
Method            | POST
Data Format       | JSON
Content type      | Application/json