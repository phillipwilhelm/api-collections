The xAPI allows developers to programmatically invoke commands and query the status of devices that run Webex RoomOS software:
- Executing commands requires an auth token with the spark:xapi_commands scope.
- Querying devices requires an auth token with the spark:xapi_statuses scope.

To manage Devices, see the Devices API. xAPI commands and statuses are described in the Cisco Collaboration Endpoint Software API Reference Guide. For more information about xAPI, see the xAPI Guide.

https://developer.webex.com/docs/api/v1/xapi

**Quick start**
- add an `access_token` to your environment
- start with the "init" folder in order to setup your environment with the first device your token has access to

Environment variables:
- [required] access_token: bot token who has been granted xAPI access (R/O or R/W) via the Webex Control Hub

Dynamically variables (computed via tests scripts):
- _deviceId: device identifier accessible from the access token
- _callId: id of the call just initiated (in order to end the call essentially)

