# Who this collection is for
Those who are trying to bring consistency to an organizations API design will be thinking about how they can bring a set of guidelines into force.

# What does this collection do?
Lays out a set of requests that allows you to assess the condition of your API schema within Postman, and whether it meets the style and criteria that you expect your APIs to present.

# More
This is the API governance Postman collection for [Union Fashion](http://union.fashion/), providing a documented and executable process that can be applied to all APIs being developed to support business operations. Demonstrating how Postman collections and tests can be used to define and enforce governance across API operations, in a self-service, and eventually fully automated way.

This governance framework is still being defined, and will keep evolving based upon the overall objectives of Union Fashion operations. [GitHub issues for teh Union Fashion governance repo](https://github.com/union-fashion/governance/issues) will be used for evolving these collections, and the individual requests that they possess. Allowing all of the individual rules to be evolved independently, but still exist as a single collection.

Each API being evaulated needs to have it's own governance environment, which is available above, providing an artifact for all the meta adata about the API being governed, and to be able to store the results the governance process, providing a snapshot of how well each API meets the governance criteria. Adding another potential environmental state to each API, helping bring each API into alignment with each other.

This governance collection is solely focused on what I would consider to be a "design governance" collection focused on the design of each API using its OpenAPI contract. There is [another governance collection being developed to scan and report upon other stops along the API lifecycle](https://documenter.getpostman.com/view/10394726/SzYUagbA?version=latest), but since most people are only discussing the design of an API when investing in API governance, I wanted a separate collection to focus on this part of the conversation.

## Configuration
There are two separate configuration options available as part of this collection. There needs to be more work to streamline how schemas are pulled from the Postman API, and until that work is done, there are to paths you can choose to configure which API you will be governing with this collection:

* Option 1 - This is a manual series of API calls you make to pull the individual API to be governed, then the version, and schema. Each individual request has it's own instructions.
* Option 2 - This is a single API call with a test script to make all of the API calls necessary, abstracting away the complextiy. You just have to provide the name of your workspace, API, and the version of the schem that you want to work with.

There used to be a version of this that would store the OpenAPI in the environment and each call would work from that, but it makes more sense to always pull the latest OpenAPI definition with each request, however there are API rate limits to consider as part of this.

Here are some other things to keep top of mind as you are working with this collection:

- **This is a proof of concept -- use at your own risk!**
- **You will need your Postman API key in the environment**
- **Make sure you have the environment selected before running**
- **Run the one of the configuration options before running anything individual requests**
- **It uses same testing infrastructure as regular API request, so view using test results tab**
- **It stores all the results of each individual test in the environment**
- **Once configured, this collection can be run as monitor or in pipeline using Newman**

If you have any questions, comments, or feedback you can submit GitHub issues for the repo, and we will work to support as part of regular work on this project. It is a proof of concept, and the scripting is very hacky, and needs has much that should be delivered as common libraries, but works for demonstrating what is possible. Feedback is necessary to know where to take this development next, helping standardize how API design governance is executed.