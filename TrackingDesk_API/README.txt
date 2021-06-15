## Authentication
All API calls require that you send your token with the call. You can get your token from the [TrackingDesk platform](https://platform.trackingdesk.com/#accesstoken). 

The prefered way is to use the "Authorization" header:
```
Authorization: Bearer {{TOKEN}}
```


The query parameter `?access_token={{TOKEN}}` is also supported.


## Base URL
The Base URL of all API calls is `https://green-node.trackingdesk.com`