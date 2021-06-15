## Uses of these API’s
Send Notification and Conversation messages through Whatsapp. These APIs can be used after the successful registration of a Whatsapp Business API number for your business.

## Basic information for Integration
{{url}} - URL supplied to access your account.

{{apiVersion}} - v1

## Supported Formats
This section explains the supported formats of the message. The following formats are only supported:

|**Type**|**Format**|
|--|--|
|template|Text message only|
|text|Maximum text message length of 4096 characters|
|image|JPG, JPEG, PNG|
|document|PDF, DOC(X), PPT(X), XLS(X) ,TXT etc|
|audio|AAC, M4A, AMR, MP3, OGG, OPUS|
|contacts|List of contacts|
|location|Current or Map location|
|video|.mp4|

> Maximum characters allowed are 4096 on a single trigger
> The maximum file upload size is 100 MB

## Authorization
Uses “appid” for the identification of the account, “integrationid” for the identification of the channel, and JSON Web Tokens (JWTs) as the authentication method for server-to-server calls.
Find the “appid”, “integrationid”, and generate JWT tokens from the "Developers" page inside your account.
Use “appid” in the API URL as  mentioned in the example
Use “integration id” in the destination details within the request body
JWT token need to be specified in the header as “bearer <JWT token>”
