Often times API requests must be executed in sequence to achieve a desired system maintenance effect or to routinely collect information. Postman Process Automator uses a custom Postman pre-request script to replicate your API requests, then use the replicated requests to provide the client with a Python automation script enabling usage inside of the Postman suite and live system computers. The Python-driven automated requests execute at identical time intervals as when you recorded the request sequence. Postman Process Automator currently supports GET, POST, PUT, DELETE, and PATCH methods of encoding payload types form-data, x-www-form-urlencoded, xml (sent as "raw" encoding), JSON (sent as "raw" encoding), or test/plain data (sent as "raw" encoding).

How to use Postman Process Automator:
1. Query the Initialize Request Sequence Recording Session endpoint to start a recording session

2. Query the Get Postman Interceptor endpoint to fetch the latest interceptor Javascript code.

3. Paste the interceptor code (with your request sequence recorder session id present as a query parameter at the top of the file) into the pre-request text-field under the url and method specifications for the requests which you wish to record (the requests do not have to be in the same collection).

4. Execute the requests as you normally would without any regard to the background PPA process analyzing your requests. Be sure to set the proper Content-Type headers!

5. Conclude the request sequence recording session by engaging the Terminate Request Sequence Recording Session endpoint.

6. Query the Get Request Sequence Recording Session endpoint for a Python file containing the code which automates the sequence of requests executed between the initialization and termination endpoint engagements.
