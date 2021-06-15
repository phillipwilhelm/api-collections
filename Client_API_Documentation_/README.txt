The API's listed in this collection have been selected as the most likely to be useful to the ABC Corp 1 project.  A full list of the Ascendon API's can be found by selecting the "Documentation" icon from the new Invision portal.

https://sbx1.invision.ascendon.tv/

NOTE:  The login credentials required to access the full online documentation are the same those required to access your SBX Invision user.  Please contact a CSG representive if the "Documentation" icon is not present once logged in.

## Architecture

The following diagram shows a high level view of the ABC Corp 1 architecture.  Ascendon API's fall within the CSG Business Layer Microservices section (highlighted with a dashed boarder).



## Ascendon JSON API Overview

* CSG's Ascendon Web Service APIs fall in to two categories: static metadata and transactional. 
* APIs are accessed via a combination of GETs or POSTs over HTTPS based on the type.  Static metadata APIs are RESTFUL APIs accessed by HTTPS GETs.  
* Transactional data (e.g. retrieving a subscriber's profile, entitlements, commerce, etc.) is accessed using a Request/Response Action approach via POSTs over HTTPS.  
* For these methods, the request object is passed as JSON in to the body of the POST.  If a method doesn't return data, it responds with an empty response.  
* If a request fails, the response will contain a Fault object with a specific error code and a developer friendly (e.g. not intended for end users) error message.  Because of certain end-consumer platform limitations, during normal processing every transactional request (succeeding or failing) replies with an HTTP 200 to ensure that the requesting application can access the error response.  
* However, in order to ensure that the CDN does not cache error responses for an extended period of time, metadata requests will respond with an HTTP 500 for any non functional error.  For example, a product not found error code will still be returned via an HTTP 200 so all platforms have access to the error code and message.  However, a general processing error will be returned as an HTTP 500.  
* The HTTP 500 will instruct the CDN to only cache the failed response for 10 seconds before attempting the same request again.  Therefore, application platforms that do not have access to non-HTTP 200 responses will have to take this in to consideration and treat an HTTP 500 as an unknown system error.

## JSON API Endpints

The Ascendon API's are organised into a number of services. The most relevent services to subscriber processing are:

* Metadata
* Subscriber
 
![Diagram to follow](http://custom.sbx1.cdops.net/Util/Screenshots/XYZ/Ascendon_API_Services.jpg)