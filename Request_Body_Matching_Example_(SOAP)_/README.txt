This collection has a single request and two saved examples representing responses for two different request bodies. 

One of the saved example is when a request is made to fetch countries in the North American continent.

The other saved example is for when a request is made to fetch countries and no continent has been specified.

The two examples differ in the request body that is sent to the `/continents` API.

To test body matching, create a Postman Mock Server on this collection and then make a request to the mock server using the request path and request body that is saved in the examples. 

Make sure you pass the `x-mock-match-request-body` header with value set to `true`.

Also make sure you pass the correct `content-type` when making this request. For this example, the `content-type` should be set to `text/xml`.

Also if you are using environment variables of the form `{{my_environment_variable}}` in your saved examples, make sure that you specify the environment that has this value while creating the mock.