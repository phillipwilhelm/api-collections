The import.io API is a RESTful API. It is designed as much as possible to have resource-oriented URLs and to use HTTP status codes to indicate API status.

We use standard HTTP which can be understood by any HTTP client, and we support CORS to allow you to interact with our API from a client-side web application. Remember, you should never expose your secret API key in any public client-side code.

JSON is always returned from the API, including errors.

import.io uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing), and codes in the 5xx range indicate an error with our servers.