**Extract data from the response**. This can be useful to capture authorization, session, or cookie data or to transform and parse information available within the response body to chain requests and use this data in a subsequent request.

Here's a [step-by-step tutorial](https://blog.getpostman.com/2018/03/19/how-to-make-money-using-postman-chaining-requests/) showing how to do this.

* Extract response body data
* Extract cookie data
* Extract session and header data
* Extract XML and transform to JSON

![[test script](https://i.imgur.com/zVrV2qS.png)](https://i.imgur.com/zVrV2qS.png)

# Get started
* **Set up an environment** so that you can save information and then use it in subsequent requests. Although you can use other types of variables, one of the more common ways of chaining requests is by using environment variables. Learn more about [managing environments](https://learning.getpostman.com/docs/postman/environments_and_globals/manage_environments). 
* **Run a folder or collection** using the [collection runner](https://learning.getpostman.com/docs/postman/collection_runs/starting_a_collection_run). You can also step through each request by hitting that blue **Send** button manually, but don't forget about the collection runner. Running folders or collections with the runner will automatically execute all your requests in a predetermined order.
 
![[using environment variables](https://i.imgur.com/WB1OWtf.png)](https://i.imgur.com/WB1OWtf.png)

# Next steps
Got the hang of chaining requests? There's a bunch more you can do with scripts.
* **Do setup and teardown for testing**. For example, you can do calculations to use in the main request or [send asynchronous requests](https://blog.getpostman.com/2017/10/03/send-asynchronous-requests-with-postmans-pm-api/). Tests scripts are the cornerstone of [testing in Postman](https://blog.getpostman.com/2017/10/25/writing-tests-in-postman/) – to validate your endpoint is working as expected.
* **Direct the next request to be called** based on the results of the server response. Using basic JavaScript, you can then use [`postman.setNextRequest("Request name")`](https://learning.getpostman.com/docs/postman/scripts/branching_and_looping/) to guide the sequence of the remaining API calls.