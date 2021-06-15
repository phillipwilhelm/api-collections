This template demonstrates the workflow described in [Building resilient APIs with chaos engineering](https://medium.com/@joycelin.codes/chaos-d3ef238ec328).

Included in this template:
* **Simulate an API outage** of critical internal APIs or external third-party APIs using a [Postman mock](https://learning.getpostman.com/docs/postman/mock_servers/intro_to_mock_servers/) to test your fallbacks by returning a failing server response. 
* **Shut down a container** on an AWS EKS cluster (and optionally roll back the attack) using [Gremlin](https://www.gremlin.com/).
* **Limit a container's resources** by creating a CPU attack using [Gremlin](https://www.gremlin.com/).

![[collection runner](https://i.imgur.com/UPPy3bQ.png)](https://i.imgur.com/UPPy3bQ.png)
 
# Get Started

For the infrastructure attack on EKS, you will need a target. To work with a sample app, deploy [Hipster Shop: Cloud-Native Microservices Demo Application](https://github.com/GoogleCloudPlatform/microservices-demo) on a Kubernetes cluster, and install [Gremlin](https://www.gremlin.com/) on your Kubernetes dashboard.

Then [update the corresponding Postman environment](https://learning.getpostman.com/docs/postman/environments_and_globals/manage_environments/#editing-an-active-environment) called `chaosEngineering` with your own credentials and app information.

| Environment Key   | Description                          |
|-------------------|--------------------------------------|
| `gremlin_api_key` | Use a team-level [Gremlin API key](https://www.gremlin.com/docs/api-reference/api-keys/) |
|`your_deployed_app_URL`| This is the URL of your deployed app |
