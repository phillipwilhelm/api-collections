The **IntelligenceBank Graph API (v3)** is the latest version of the **IntelligenceBank Public API**.

The calls listed below all work in conjunction with the **IntelligenceBank API (v2) login calls**, which are listed on this page under [**Authentication (v2)**](https://apidoc.intelligencebank.com/?version=latest#2aeafa0c-8d75-49be-8a61-4677da2cab80) for easy reference. To get started, you will need to retrieve the [API v2 URL (apiV2url)](https://apidoc.intelligencebank.com/?version=latest#fdd1d62c-27dc-4c72-94c9-396ac8006bc8).

The IntelligenceBank API (v2) documentation can also be accessed [here](https://intelligencebank.atlassian.net/wiki/spaces/APIDOC/overview) for reference. Note that some calls are still pending migration to the v3 API.

On the **Login** call response ([Standard](https://apidoc.intelligencebank.com/?version=latest#d9ead492-1df9-4ea9-babf-06690a168dce) or [Browser](https://apidoc.intelligencebank.com/?version=latest#a01345b8-e9c4-4f39-9c83-a0f4e2519b02) methods), the following parameters are to be used in subsequent v3 calls:

*   **"apiV3url"**: this is the v3 API server URL, and the root URL of all API calls.
    
*   **"sid"**: this is the session id. It is to be added to the Headers. It will be valid for the length of the user session.
    
*   **"clientid"**: this is the client id and unique to your platform. It is to be added to the request URL for GET requests, or to the body part for POST requests.
    

How to use this Collection with Postman?
========================================

*   **Import** the Collection into Postman by clicking **Run in Postman** on the top right of this page.
    
*   The Collection is configured to **populate as many parameters as possible automatically** so that you can get started easily with using these API calls.
    
*   Click the "Eye" icon on the top right, and modify the following values of the **API Default** environment, under the CURRENT VALUE column:
    
    *   **{{platformurl}}**: Enter your IntelligenceBank platform URL (without https://)
        
    *   **{{emailaddress}}**: Enter your IntelligenceBank username/email address
        
    *   **{{password}}**: Enter your IntelligenceBank password
        
*   **Leave all other parameters unchanged** as these will populate automatically by triggering the following 2 API calls:
    
    *   [Get V2 API URL (apiV2url)](https://apidoc.intelligencebank.com/?version=latest#fdd1d62c-27dc-4c72-94c9-396ac8006bc8): click Send to auto-populate the {{apiV2url}} parameter value. This is required for the next call to work.
        
    *   Standard Login (v2): click Send to auto-populate the other parameters.
        
*   All parameters displayed in orange in the calls should now be mapped to values.
    
*   Only parameters displayed in red (e.g. {{file\_id}}) will require manual input.
    
*   NOTE: if you are login in to your platform via Single Sign On and/or 2 Factor Authentication, use the [Browser Login](https://apidoc.intelligencebank.com/?version=latest#a01345b8-e9c4-4f39-9c83-a0f4e2519b02) method to authenticate instead.


![enter image description here](https://cdn.intelligencebank.com/au/share/2yO/JnzLwa/16Xkbp/preset=AEXK6e/Environment+Config)

Common Error Responses
======================

|     |     |     |     |
| --- | --- | --- | --- |
| **ERROR CODE** | **DEFINITION** | **ERROR MESSAGE(S)** | **VERBOSE** |
| **401 UNAUTHORIZED** | Your authentication session has expired. | error.authentication.required | “No valid session. Authentication is required” |
| **403 FORBIDDEN** | When the user does not have permission to do the action on and/or access to the requested item. | "error.no\_permission" | “No Permission” |
| **404 NOT FOUND** | When the provided \_id or id value does not exist or is for an archived item. | "error.not\_found"<br><br>"error.folder.parent.not\_found"<br><br>"error.resource.not\_found"<br><br>“error.record.not\_found”<br><br>“error.{{object}}.not\_found” | “Not Found”<br><br>“Parent folder not found”<br><br>“Resource not found”<br><br>“Record not found”<br><br>“{{Object}} not found” |
| **400 BAD REQUEST** | When the request parameters or body has invalid data. | "error.service.query\_params.invalid"<br><br>“{{field}}": { "error.validator.empty": null }<br><br>“{{select\_field}}": { "Value must be a match": null }<br><br>"{{date\_field}}": { "error.validator.is\_date": { "value": "{{wrong\_value}}" } | "Bad request - query parameters are invalid"<br><br>"{{field}}": { "This field cannot be empty": null }<br><br>“{{select\_field}}": { "Value must be a match": null }<br><br>"{{date\_field}}": { "Value must be a valid date": { "{{wrong\_value}}": "" } |
