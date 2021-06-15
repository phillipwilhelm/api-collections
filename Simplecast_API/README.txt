Simplecast's API makes it possible for you to customize your podcasting experience. What do you want to build? Manage your shows, episodes, and discover more with analytics using our powerful platform.

This document gives you the tools you need to start building. Our API is self-describing. Each response gives your app all the information it needs to perform related actions.

### Get Started 
The API can be accessed at

`https://api.simplecast.com`

### Authentication 
Get your api token from your Private Apps page. Then, with each request, include your api token as your bearer token in the authentication header, e.g.

authorization: Bearer {token} 

### Pagination 
To page responses on list endpoints, you can use query parameters "limit" and "offset".

`https://api.simplecast.com/podcasts/:podcast_id/episodes?limit=12&offset=0` 

Limit denotes the maximum number of objects to return, while offset specifies where to start the page.

### Versioning 
At this point, there is one version for the Simplecast API, which the following endpoints hit. We will add a versioning option to the header soon. But, rest assured, we won't make any breaking changes in the meantime.

Note: if you have migrated from legacy Simplecast to the new Simplecast, your access to the legacy API will continue to function, but after migration, any new data (both episodes and analytics) will only be accessible through the current API.

### Endpoints 
Each endpoint returns actions options in the form of JSON based on the access of the user or client. Each action option is described with a URL, inputs, and HTTP method.