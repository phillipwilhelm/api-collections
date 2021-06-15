![](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/images/K8s-AWS-Postman.png?raw=true)

> The following template is accompanied by [this](https://blog.postman.com/kubernetes-tutorial/) blog post

Kubernetes is open source and useful for container orchestration. In this tutorial, we are going to use Postman collections to learn Kubernetes and use it's API to deploy an app on a Kubernetes cluster hosted on AWS.

This is a hands-on tutorial. Don't fret if you are not familiar with Kubernetes and containerization. We aim to deliver the following through this tutorial:

☸️ Prerequisites <br>
☸️ Brief Overview on Containers <br>
☸️ Enter Kubernetes <br>
☸️ Creating a Kubernetes cluster <br>
☸️ Accessing the Kubernetes API from Postman <br>
☸️ Authorising Postman Collection <br>
☸️ Deploy an app <br>
☸️ Expose your App <br>
☸️ Clean up <br>
☸️ What Next?

**Note**: We will be creating the Kubernetes cluster on AWS EKS, but you can also follow the tutorial with a cluster hosted on any other cloud providers or locally using Minikube.  

# Prerequisites
Familiarity with REST APIs would be required. In addition you also need the following: 
- Create an [AWS account](https://portal.aws.amazon.com/billing/signup?refid=em_127222&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) 
- [Install](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) and [configure aws cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html) - Required to configure credentials

- [Install eskctl](https://eksctl.io/introduction/#installation) - a command utility to interact and create the cluster on EKS
- [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) - command line utility to work with Kubernetes clusters
- Clone [Github repository](https://github.com/meenakshi-dhanani/k8s-postman-tutorial) - Contains .yaml files required in upcoming sections
- Create your Amazon Cluster IAM role to access the cluster
- Setting up Amazon EKS cluster VPC

This is a good guide that has all of the prerequisites mentioned above and instructions to install them - https://docs.aws.amazon.com/eks/latest/userguide/getting-started-console.html

# Brief Overview on Containers
Are you familiar with the ***but it works on my machine*** problem? A lot of times your application does not perform as it does in your local environment, it may be because the production environment may have different versions of the libraries, a different operating system, different system dependencies, etc. Containers provide you with a sustainable environment because your application now runs in a box (container) that includes all dependencies required by your app to run and is isolated from other applications running in other containers. They are preferred over VMs since they use operating system level virtualization and are lighter than VMs. [Docker](https://www.docker.com/products/container-runtime) can be used as container runtime. 

![Benefits of Containerization](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/images/Benefits%20of%20Containerization.png?raw=true)
# Enter Kubernetes

Each app/service nows runs in a container, thus there can be separation of concerns. Services need not be intertwined with each other and a microservices architecture would work best with containerization. We have established why the world is moving towards containers, but who is going to manage these containers, how to do you rollout a release? How do you run health checks against your services, and get them back up if they are failing? Kubernetes does it all for you. It automates all of this. You can easily scale up and scale down your services with Kubernetes. 

![Kubernetes Benefits](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/images/Kubernetes%20Benefits.png?raw=true)

You could use kubernetes anywhere for on-premise deployments or even hybrid clouds. For instance, you could have your cluster on GCE, AWS, Azure any cloud providers. For this tutorial, let's create a kubernetes cluster on AWS.

You can read more about the benefits of containerization and container orchestration with Kubernetes [here](https://cloud.google.com/containers). This is a really enthralling space, especially for folks interested in DevOps.


# Creating a Kubernetes cluster
Assuming you have followed the steps in the prerequisites section, you should have eksctl installed. 
Let's try out the following command to check if eksctl can successfully access the AWS account and list existing clusters if any.
```
eksctl get cluster --region us-east-1
```
In case this command fails, you may want to make sure your credentials are set up correctly as mentioned [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html).

Next, we must create a cluster and assign some resources to it. The [cluster.yaml](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/cluster.yaml) is present in the github project we cloned as mentioned in the prerequisites.

You can customise the configuration for the cluster based on the resources you want to assign to your cluster. You could choose a different region, maybe add more nodes or also a different instance type. For the purpose of this tutorial, we do not need as much CPU or memory. 

```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: playground
  region: us-east-1

nodeGroups:
  - name: ng-1
    instanceType: t2.small
    desiredCapacity: 2
```
You could choose a different region, may be add more nodes or also a different instance type. For the purpose of this tutorial, we do not need as much CPU or memory. 

**A word of caution**: The pricing for larger instances and more number of nodes would be more. 

Use the following command to create the cluster:
```
eksctl create cluster -f cluster.yaml
```

It may take a while for the set up. Once this command succeeds, assuming you have kubectl installed, the configuration for kubectl to access the cluster would be stored in `~/.kube/config`. Try fetching the nodes on the cluster using kubectl.

```
kubectl get nodes
```
You should be able to see the two nodes. 

# Accessing the Kubernetes API from Postman
Next, we require a service account to communicate with the Kubernetes API. The service account is authorised to perform certain actions eg. creating deployments, listing services by attaching it to a cluster role. 

Run the following command to create a service account.

```
kubectl create serviceaccount postman
```
We must create a role definition for the service account. This role definition specifies all actions that are permitted on the resources mentioned. The [role.yaml](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/role.yaml) is present in the github project we cloned as mentioned in the prerequisites.
```
role.yaml
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1beta1
metadata:
  name: postman-role
rules:
- apiGroups: ["apps", ""] # "" indicates the core API group
  resources: ["pods", "services", "deployments"]
  verbs: ["get", "watch", "list", "create", "update", "delete"]
```
We are configuring actions that can be performed on resources. We'll look at what these resources mean and how to create them in the next steps.

Run the following command to create the role.
```
kubectl apply -f role.yaml
```

We must assign the role to the service account by creating a role-binding.

```
kubectl create rolebinding postman:postman-role --clusterrole postman-role --serviceaccount default:postman
```

For every service account created there is a secret token. Finally, we must extract the following from the token created for the service account:
- API server URL
- Bearer Token
- CA Certificate

```
kubectl describe serviceaccount postman
```
This command should reveal the secret eg. postman-token-9lxcc

Next, we must describe the secret.

`kubectl get secret <secret-token> -o json`

This command should reveal the ca.crt and the token inside a data object. We need to decode these to base64 and use them. This could be simplified using [jq](https://stedolan.github.io/jq/download/) command line utility.

```
# Extract the token from the Secret and decode 
TOKEN=$(kubectl get secret <secret-token> -o json | jq -Mr '.data.token' | base64 -d)
# Extract, decode and write the ca.crt to a file
kubectl get secret <secret-token> -o json | jq -Mr '.data["ca.crt"]' | base64 -d > ca.crt
```

You must get the API server URL from Amazon EKS. If you log into your Amazon account and see the cluster details for the `playground` cluster we created, you should find an **API server endpoint**. That is the URL for the API server that we are going to be hitting via Postman.

![API Server Endpoint on AWS cluster](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/images/AWS-endpoint.png?raw=true)

# Authorising Postman Collection 
Import the collection into Postman and select the Manage Environments button on the top right and edit the following:

![Edit AWS Environment](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/images/Edit%20AWS%20Environment.png?raw=true)

Paste the API Server Endpoint into the *CURRENT VALUE* for kube-api-server and the token into auth-token *CURRENT VALUE*. Click on *Update* 

**Tip**: The current value is never shared while sharing the Postman collection. Also, since these variables have sensitive information, it is best to add them to the environment variables. We could use the same collection and run it on a different environments eg. GCP, Minikube.

Next, add *Authorization* to the collection. Adding *Authorization* at the collection level will ensure all the requests will be authorised with the same token/credentials. 

Click on *Edit* for the collection and under the *Authorization* see how the Bearer token will be passed in the Request Headers for each request.

![Edit Authorization](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/images/Collection%20Authorization.png?raw=true)


Almost there! The last step to get our collection ready is adding the CA Certificate. This can simply be done by clicking on Settings for Postman and under Certificates, turn on the CA Certificate toggle and upload the ca.crt file we created. Alternatively you could disable certificate verification, but that is not recommended.

![Upload CA Certificate](https://github.com/meenakshi-dhanani/k8s-postman-tutorial/blob/main/images/Upload%20CA%20Certificate.png?raw=true)
   