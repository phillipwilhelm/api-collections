Enumerate social media accounts using Postman! Last updated 2021-01-24T13:01:48.387Z, with 271 service(s).


Inside the `Postman Sherlock` collection, a corresponding Postman Request item is created for each web service that Sherlock supports.

Once a username is supplied via environment variables, the request item is able to test if the username has been taken on the web service by [checking the response status code or looking for an error message inside the response body](https://github.com/sherlock-project/sherlock/blob/master/sherlock/sherlock.py#L321). 

By running the entire collection at once and inspecting the tests that passed, you can enumerate the accounts on various webservices that are tied to the same username!

### Setup & Running

To just enumerate the known accounts of a single user, set up a environment with a single variable `username`, with any value you want, then run the entire `Postman Sherlock` collection.

Be careful when running this in Postman Web, it involves almost 300 requests and can take quite a hit on your webagent quota! We also highly recommend you disable response and cookie saving.
