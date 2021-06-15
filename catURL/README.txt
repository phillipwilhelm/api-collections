We'll start with a simple Node app that functions like a URL shortener. In our case, we'll transform one URL into a different one using cat verbs, cat adjectives, and cat emojis 🐱 - and when you input your custom URL into a browser, you'll be redirected back to the original website.

![[catURL website](https://i.imgur.com/yypLUxZ.jpg)](https://i.imgur.com/yypLUxZ.jpg)

### Get started

This collection and environment was originally used as an example in [Deploying a scalable web application with Docker and Kubernetes](https://medium.com/@joycelin.codes/deploying-a-scalable-web-application-with-docker-and-kubernetes-a5000a06c4e9) from the [Postman Engineering blog](https://medium.com/postman-engineering).

If you want to follow along, go ahead and fork [this example](https://github.com/postmanlabs/node-doc-kube) and follow the README steps to spin up a local version of these APIs. 

The beauty of using containers is that even if I'm developing this example on a machine with my Operating System and a different version of Node, you can rely on my container image to prescribe the exact specifications you'll need to run the same application seamlessly on your machine, or in the cloud, or wherever you choose to deploy.

### Test the redirect

Since we're working with redirects, let's set up Postman so we can properly test these requests. By default, Postman will follow a redirect -- unless we tell it not to. If we update our general Postman settings to disallow redirects, we can inspect our server's response headers before the redirection.

* To run the `redirect test` request, make sure you have `Automatically follow redirects` toggled OFF under the general [Postman app settings](https://learning.getpostman.com/docs/postman/launching_postman/settings#general-settings). 
* To run the collection in the Postman app via [collection runner](https://learning.getpostman.com/docs/postman/collection_runs/starting_a_collection_run), make sure you have the same `Automatically follow redirects` toggled OFF.
*  To run the collection using Postman's command line runner [Newman](https://github.com/postmanlabs/newman), make sure you include the flag `--ignore-redirects ` with your command.
*  To run the collection from the Postman cloud using a [monitor](https://learning.getpostman.com/docs/postman/monitors/setting_up_monitor), make sure you check the box that says `Don't follow redirects`.

