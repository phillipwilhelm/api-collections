From this blog post about [using Postman to write to your local file system](insert link here), this is an example of pulling data from this [open source REST API for SpaceX data](https://github.com/r-spacex/SpaceX-API), and writing to a local file.

### Quickstart

1. Write a script that listens for POST requests and writes payloads to your local file system. Here's [a node.js example](https://gist.github.com/loopDelicious/213881bc1d4c8f64e1404aa7c7cbb413).
2. Install any dependencies, run the script, and start your local server.
  [![run local server](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/localServerRun.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/localServerRun.png)
3. Run this Postman collection that submits a GET request for launch data and then submits a POST request to your local server.
  [![collection runner](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/localServerCollectionRunner.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/localServerCollectionRunner.png)