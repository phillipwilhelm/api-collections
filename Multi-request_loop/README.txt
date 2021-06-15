This Collection gets a list of IDs, then loops through 3 POST requests that submit these IDs until there are none left.

The layout is as follows:


**GET ID list:** https://postman-echo.com/get

Description:
- response contains an array of numbers to use as dummy data.


Test script:
- Parse IDs out of JSON, and store them as an array
- `JSON.stringify()` the array and store in an environment using `pm.environment.set('key',value)`;
- Store the length of the array in the environment

**1st POST request:** https://postman-echo.com/post?test1={{id}}

Description:
- A request meant to do something with the IDs we get in the **GET ID list** request.
- Also contains a pre-request script that is critical for looping through the data above


Pre-request script:
- Check for/declare a counter variable in the environment using `pm.environment.has('key')`, and `pm.environment.set('key',value)` (this is so you can iterate through the array you stored when looping requests)
- Parse the array stored in the environment, and set value for the `{{id}}` variable based on the index of the array you're iterating through
- Increment your counter, and update the environment variable with the new value (`pm.environment.set('key',value);`)

**2nd POST request:** https://postman-echo.com/post?test2={{id}}

Description:
- A request meant to do something with the IDs we get in the **GET ID list** request.


**3rd POST request:** https://postman-echo.com/post?test3={{id}}

Description:
- A request meant to do something with the IDs we get in the **GET ID list** request.
- Also contains a test script, which facilitates the looping of the 3 get requests in this Collection.

Test script:
- Check the length of the parsed array against your counter variable, and if there are more indexes use `postman.setNextRequest('request_name')` to loop back to the 2nd request in the Collection.