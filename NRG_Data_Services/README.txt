# Overview
NRG Data Services consist of APIs for converting, uploading and managing SymphoniePRO RLD files in the cloud.

# Authentication
Users will need a Client Id and Secret to use any of the requests. Client Id and Secret are available at the [NRG Data Services](https://nrgdataservices.azurewebsites.net/ ) portal.

Use the **RetrieveToken** API with the Client Id and Secret to get a bearer token. The token is then used for authorization in subsequent requests.

# The APIs