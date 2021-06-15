This is an example of how to run the contents of only a specific folders with a Monitor, using Scripts.

Credit to @JohnArrowwood on GitHub for the idea of using a dummy request at the top of the Collection as a logic gate. :)

https://github.com/postmanlabs/postman-app-support/issues/5707#issue-395314656


**NOTE:** because there isn't a [SandboxAPI](https://learning.getpostman.com/docs/postman/scripts/postman_sandbox_api_reference/) method for specifying a folder as a next request target, the folders in this example are really just for ease of organization. This approach works the same without your requests being grouped in folders, but folders makes it easier to keep track of them and mentally organize your workflow. :)

# Why?
This approach allows a single Collection to be maintained, with different behavior defined by the environment included with it. This way, a single Collection with muliple test suites can be used, and different parts of it executed by different monitors.

# How it works

In the environment included, set `first_request` to the _exact_ name of the first request you want to run, and `last_request` to the last request you want sent before the Collection run is ended.

Make sure to keep the folder `logic` at the top of the Collection. The folders `echo1` and `echo2` can be deleted and replaced with whatever requests you want. They're included as an example.

**Example:** the folder `echo1` in this Collection contains three requests: `echo1a`, `echo1b`, and `echo1c`. In the environment included, `echo1a` is the value for `first_request`, and `echo1c` is the value for the second request. When the Collection runs:

1) The request in `logic` is sent (dummy request, sent to example.com). This is needed so that the Test script on the Collection can set the first "real" request to send.  

2) The Test script on the Collection sets the first "real" request to what is specified in the `first_request` environment variable, in this case: `echo1a`.  

3) Requests will continue being sent, as they normally would during a Collection run. In this example, `echo1b` will be sent because it's the next in order. The Test script on the Collection will check to see if each request being sent is the `last_request` specified in the environment.  

4) When the request specified in `last_request` is sent (in this case, `echo1c`), the Test script on the Collection will end the Collectio run after the request has finished.

The following feature request has some great discussion around logic nodes and other workflow automation:

https://github.com/postmanlabs/postman-app-support/issues/5707