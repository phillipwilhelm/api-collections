# Who this collection is for?

* Someone who wants to programmatically build out the different elements ( [Workspaces, API's, Mocks, Collections, Monitors) that are required during a typical API Lifecycle using the [Postman API](https://learning.postman.com/docs/developer/intro-api/).
* Someone who wants to customize their Postman environment on their CI/CD build pipelines using the [Newman Collection runner](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/) for their specific workflows and use case scenarios

# What does this collection do?

It enables us to perform the below operations programmatically:

* [Create a Workspace](https://learning.postman.com/docs/collaborating-in-postman/using-workspaces/creating-workspaces/)
* [Create a API](https://learning.postman.com/docs/designing-and-developing-your-api/the-api-workflow/#creating-an-api)
* [Version a API](https://learning.postman.com/docs/collaborating-in-postman/versioning-an-api/)
* [Define an API](https://learning.postman.com/docs/designing-and-developing-your-api/the-api-workflow/#defining-an-api)
* [Generate collections from an API Schema](https://learning.postman.com/docs/designing-and-developing-your-api/the-api-workflow/#generating-a-collection)
* [Create an Environment](https://learning.postman.com/docs/designing-and-developing-your-api/the-api-workflow/#adding-an-environment)
* [Add a Mock Server](https://learning.postman.com/docs/designing-and-developing-your-api/the-api-workflow/#adding-a-mock-server)
* [Observe an API](https://learning.postman.com/docs/designing-and-developing-your-api/the-api-workflow/#observing-an-api)

To implement operations required during a typical API Lifecycle using the Postman API, you can navigate to the [Postman API documentation](https://documenter.getpostman.com/view/631643/JsLs/) to find the list of possible operations using the Postman API

## Setup
We would be required to:
1.  [Generate an API Key](https://learning.postman.com/docs/developer/intro-api/#generating-a-postman-api-key). 
2. [Create an Environment](https://learning.postman.com/docs/sending-requests/managing-environments/#creating-environments)
3. [Select an active Environment](https://learning.postman.com/docs/sending-requests/managing-environments/#selecting-an-active-environment)

Once we have performed the above actions, we can either:
3. Execute each request by hitting the [Send](https://learning.postman.com/docs/getting-started/sending-the-first-request/#sending-a-request) button on each request or
2. Execute all the requests in a collection sequentially using the [Collection Runner](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/) 

If we wish to execute the collection runner on the command line or on the CI/CD Pipeline which will enable us to perform operations essential to our API Lifecycle, we can always use the [Newman CLI](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/)
To learn about all the operations available for the Postman API, you can navigate to: https://docs.api.getpostman.com/