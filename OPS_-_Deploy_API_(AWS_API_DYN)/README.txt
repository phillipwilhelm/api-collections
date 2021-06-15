This is a collection for deploying an API from Postman to AWS API Gateway. It was distilled down from a larger API life cycle collection I am building but I wanted to pull out and let it stand on its own. Currently it is a five step deployment process.

All of this could easily be distilled down into a single Postman request, but I want to pause and make sure that is what I need. It has already been distilled down from multiple API calls to Postman, AWS DynamoDB, and AWS API Gatway. So, I am just pausing to make sure of the workflow I want for deploying an API to a development or production environment.

This collection depends on this environment to authenticate with the Postman API, AWS DynamodDB API, and AWS API Gateway API, as well as to store data used in the deployment process. You can import this environment into your Postman, enter your keys and tokens, and it should work as long as your AWS IAM is configured properly to work with AWS API Gateway and AWS DynamoDB.

If you need an OpenAPI to test out, I have ran this collection against the following APIs so far:

- [Products](https://github.com/union-fashion/products/blob/master/products-v1.json)

I will keep working on stablizing and streamling this collection, and publishing any changes as part of this documentation. Using these docs as a complete set of instructions for how to use this collecton for deploying APIs.