Let’s start with the data from a supermarket chain’s store finder and create a very simple *“Powered by FIWARE”* application by passing in the address and location of each store as context data to the FIWARE context broker.

The `docker-compose` file for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Getting-Started/icon/GitHub-Mark-32px.png) [FIWARE 101: An Introduction to the FIWARE Platform](https://github.com/Fiware/tutorials.Getting-Started)

# Architecture

Our demo application will only make use of one FIWARE component - the [Orion Context Broker](https://catalogue.fiware.org/enablers/publishsubscribe-context-broker-orion-context-broker) . Usage of the Orion Context Broker is sufficient for an application to qualify as *“Powered by FIWARE”*.

Currently, the Orion Context Broker  relies on open source [MongoDB](https://www.mongodb.com/) technology to keep persistence of the context data it holds. Therefore, the architecture will consist of two elements:

* The  Orion Context Broker server which will receive requests using NGSI
* The underlying MongoDB database associated to the Orion Context Broker server

Since all interactions between the two elements are initiated by HTTP requests, the entities can be containerized and run from exposed ports. 

![](https://fiware.github.io/tutorials.Getting-Started/img//architecture.png)

# Prerequisites

## Docker

To keep things simple both components will be run using [Docker](https://www.docker.com). **Docker** is a container technology which allows to different components isolated into their respective environments. 

* To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
* To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
* To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)



# Starting the Containers

## Initialization

First  pull the necessary Docker images from Docker Hub and create a network for our containers to connect to:

```console 
docker pull mongo:3.6
docker pull fiware/orion
docker network create fiware_default
```

## Start Up

A Docker container running a MongoDB database can be started and connected to the network with the following command:

```console
docker run -d --name=context-db --network=fiware_default \
  --expose=27017 mongo:3.6 --bind_ip_all --smallfiles
``` 

The Orion Context Broker can be started and connected to the network with the following command:

```console
docker run -d --name orion  --network=fiware_default \
  -p 1026:1026  fiware/orion -dbhost context-db
```   

You can check if the Orion Context Broker is running by making an HTTP request to the exposed port:

```console
curl -X GET http://localhost:1026/version
```

Alternatively run all your curl commands from within the container network:

```console
docker run --network fiware_default --rm appropriate/curl -s \
  -X GET http://orion:1026/version
```

**What if I get an error response?**

If you get an error response, the Orion Content Broker cannot be found where expected
for this tutorial  - you will need to substitute the URL and port in each Postman request 
with the corrected ip address. All the Postman requests in this tutorial assume 
that orion is available on `localhost:1026`. 
 
Try the following remedies:

* To check that the dockers container are running try the following:

```console
docker ps
```

You should see two containers running. If orion is not running, you can restart the 
containers as necessary. This command will also display open port information.

* If you have installed [`docker-machine`](https://docs.docker.com/machine/) and [Virtual Box](https://www.virtualbox.org/), you will need to retrieve the virtual host ip as shown:

```console
curl -X GET http://$(docker-machine ip default):1026/version
```

If you need to update the location of orion:

1. Click on the elipsis `...` at the head of the imported postman collection
2. Select `edit` from the dropdown
3. Click on the `variables` tab and alter the value from `localhost:1026` as necessary.