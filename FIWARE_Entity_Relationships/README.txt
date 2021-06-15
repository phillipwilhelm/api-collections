This tutorial builds on the data created in the previous [store finder example](http://fiware.github.io/tutorials.Getting-Started/) and creates and associates a series of related data entities to create a simple stock management system.

The `docker-compose` file for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Entity-Relationships/icon/GitHub-Mark-32px.png) [FIWARE 102: Batch Commands and Entity Relationships](https://github.com/Fiware/tutorials.Entity-Relationships)

# Data Entities

Within the FIWARE platform, an entity represents the state of a physical or conceptural object which exists in the real world.

## Entities within a stock management system

For a simple stock management system, we will only need four types of entity. The relationship between our entities is defined as shown:

![](https://fiware.github.io/tutorials.Entity-Relationships/img/entities.png)

* A **Store** is a real world bricks and mortar building. Stores would have properties such as:
  + A name of the store e.g. "Checkpoint Markt"
  + An address "Friedrichstraße 44, 10969 Kreuzberg, Berlin"
  + A phyiscal location  e.g. *52.5075 N, 13.3903 E*
* A **Shelf** is a real world device to hold objects which we wish to sell. Each shelf would have properties such as:
  + A name of the shelf e.g. "Wall Unit"
  + A phyiscal location  e.g. *52.5075 N, 13.3903 E*
  + A maximum capacity
  + An association to the store in which the shelf is present
* A **Product** is defined as something that we sell - it is conceptural object. Products would have properties such as:
  + A name of the product e.g. "Vodka"
  + A price e.g. 13.99 Euros
  + A size e.g. Small
* An **Inventory Item** is another conceptural entity, used to assocate products, stores, shelves and physical objects. It would have properties such as:
  + An assocation to the product being sold
  + An association to the store in which the product is being sold
  + An association to the shelf where the product is being displayed
  + A stock count of the quantity of the product available in the warehouse
  + A stock count of the quantity of the product available on the shelf


As you can see, each of the entities defined above contain some properties which are liable to change. A product could change its price, stock could be sold and the shelf count of stock could be reduced and so on.


# Architecture

This application will only make use of one FIWARE component - the [Orion Context Broker](https://catalogue.fiware.org/enablers/publishsubscribe-context-broker-orion-context-broker). Usage of the Orion Context Broker is sufficient for an application to qualify as *“Powered by FIWARE”*.

Currently, the Orion Context Broker relies on open source [MongoDB](https://www.mongodb.com/) technology to keep persistence of the context data it holds. Therefore, the architecture will consist of two elements:

* The Orion Context Broker server which will receive requests using NGSI
* The underlying MongoDB database associated to the Orion Context Broker server

Since all interactions between the two elements are initiated by HTTP requests, the entities can be containerized and run from exposed ports. 

![](https://fiware.github.io/tutorials.Entity-Relationships/img/architecture.png)

The necessary configuration information can be seen in the services section of the associated `docker-compose.yml`  file:

```yaml
  orion:
    image: fiware/orion:latest
    hostname: orion
    container_name: orion
    depends_on:
      - context-db
    networks:
        - default
    expose:
        - "1026"
    ports:
        - "1026:1026"
    command: -dbhost context-db -logLevel DEBUG
```

```yaml
  context-db:
    image: mongo:3.6
    hostname: context-db
    container_name: context-db
    expose:
        - "27017"
    ports:
        - "27017:27017"
    networks:
        - default
    command: --bind_ip_all --smallfiles
```

Both containers are residing on the same network - the Orion Context Broker is listening on Port `1026` 
and MongoDB is listening on the default port `271071`. Both containers are also exposing the same ports
externally - this is purely for the tutorial access - so that cUrl or Postman can access them without
being part of the same network. The command line initialization should be self explanatory.

# Prerequisites

## Docker

To keep things simple both components will be run using [Docker](https://www.docker.com). **Docker** is a container technology which allows to different components isolated into their respective environments. 

* To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
* To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
* To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A [YAML file](https://raw.githubusercontent.com/Fiware/tutorials.Entity-Relationships/master/docker-compose.yml) is used configure the required
services for the application. This means all container sevices can be brought up in a single commmand. Docker Compose is installed by default as part of Docker for Windows and  Docker for Mac, however Linux users will need to follow the instructions found [here](https://docs.docker.com/compose/install/)

## Cygwin 

We will start up our services using a simple bash script. Windows users should download [cygwin](www.cygwin.com) to provide a command line functionality similar to a Linux distribution on Windows. 


# Start Up

All services can be initialised from the command line by running the bash script provided within the repository:

```bash
./services start
```