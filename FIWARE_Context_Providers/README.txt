This tutorial builds on the **Store** entity created in the previous [stock management example](https://github.com/Fiware/tutorials.CRUD-Operations/) and enables a user to 
retrieve data about a store which is not held directly within the Orion Context Broker.

The `docker-compose` file for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Context-Providers/icon/GitHub-Mark-32px.png) [FIWARE 104: Registering Context Providers](https://github.com/Fiware/tutorials.Context-Providers)

# Context Providers

> "Knowledge is of two kinds. We know a subject ourselves, or we know where we can find information about it."
>
> — Samuel Johnson (Boswell's Life of Johnson)


Within the FIWARE platform, an entity represents the state of a physical or conceptural object which exists in the real world. 
For example, a **Store** is a real world bricks and mortar building.

The context data of that entity defines the state of that real-world object at a given moment in time. 

In all of the tutorials so far, we are holding all of the context data for our **Store** entities directly within the Orion 
Context Broker, for example stores would have attributes such as:

* A unique identifier for the store e.g. `urn:ngsi-ld:Store:002`
* The name of the store e.g. "Checkpoint Markt"
* The address "Friedrichstraße 44, 10969 Kreuzberg, Berlin"
* A physical location  e.g. *52.5075 N, 13.3903 E*

As you can see, most of these attributes are completely static (such as the location) and the others are unlikely to be
changed on a regular basis - though a street could be renamed, or the store name could be rebranded.

There is however another class of context data about the **Store** entity which is much more dynamic, information such as:

* The current temperature at the store location
* The current relative humidity at the store location
* Recent social media tweets regarding the store 

This information is always changing, and if it were held in a database, the data would always be out-of-date. To keep the context
data fresh, and to be able to retrieve the current state of the system on demand, new values for these dynamic data attributes will 
need to be retrieved whenever the entity context is requested.

Smart solutions are designed to react on the current state of the real-world. They are "aware" since they rely on dynamic data readings from 
external sources (such social media, IoT sensors, user inputs). The FIWARE platform makes the gathering and presentation of real-time 
context data transparent, since whenever an [NGSI](https://swagger.lab.fiware.org/?url=https://raw.githubusercontent.com/Fiware/specifications/master/OpenAPI/ngsiv2/ngsiv2-openapi.json) request is made to the Orion Context
Broker it will always return the latest context by combining the data held within its database along with real-time data readings from 
any registered external context providers.

In order to be able to fulfil these requests, the Orion Context Broker, must first be supplied with two types of information:

* The static context data held within Orion itself  (*Entities that Orion "knows" about*) 
* Registered external context providers associated with existing entities (*Entities that Orion can "find information" about*) 


## Entities within a stock management system


Within our simple stock management system, our **Store** entity currently returns `id`, `name`,  `address` and `location` attributes. 
We will augment this with additional real-time context data from the following free publicly available data sources:

* The temperature and relative humidity from the [Weather Underground API](https://www.wunderground.com/weather/api/d/docs?MR=1)
* Recent social media tweets regarding the store from the [Twitter API](https://developer.twitter.com/](https://developer.twitter.com/)

The relationship between our entities is defined as shown:

![](https://fiware.github.io/tutorials.Context-Providers/img/entities.png)

# Architecture

This application will only make use of one FIWARE component - the [Orion Context Broker](https://catalogue.fiware.org/enablers/publishsubscribe-context-broker-orion-context-broker). Usage of the Orion Context Broker is sufficient for an application to qualify as *“Powered by FIWARE”*.

Currently, the Orion Context Broker relies on open source [MongoDB](https://www.mongodb.com/) technology to keep persistence of the context data it holds. 
To request context data from external sources, we will now need to add a simple Context Provider NGSI proxy.


Therefore, the architecture will consist of three elements:

* The Orion Context Broker server which will receive requests using [NGSI](https://swagger.lab.fiware.org/?url=https://raw.githubusercontent.com/Fiware/specifications/master/OpenAPI/ngsiv2/ngsiv2-openapi.json)
* The underlying MongoDB database associated to the Orion Context Broker server
* The Context Provider NGSI proxy which will will:
  + receive requests using [NGSI](https://swagger.lab.fiware.org/?url=https://raw.githubusercontent.com/Fiware/specifications/master/OpenAPI/ngsiv2/ngsiv2-openapi.json)
  + makes requests to publicly available data sources using their own APIs in a proprietory format 
  + returns context data back to the Orion Context Broker in [NGSI](https://swagger.lab.fiware.org/?url=https://raw.githubusercontent.com/Fiware/specifications/master/OpenAPI/ngsiv2/ngsiv2-openapi.json) format.

Since all interactions between the elements are initiated by HTTP requests, the entities can be containerized and run from exposed ports. 

![](https://fiware.github.io/tutorials.Context-Providers/img/architecture.png)

The necessary configuration information for the **Context Provider NGSI proxy** can be seen in the services section the of the associated `docker-compose.yml`  file:

```yaml
  context-provider:
    image: fiware/cp-web-app:latest
    hostname: context-provider
    container_name: context-provider
    networks:
        - default
    expose:
        - "3000"
    ports:
        - "3000:3000"
    environment:
        - "DEBUG=proxy:*"
        - "PORT=3000" 
        - "CONTEXT_BROKER=http://orion:1026/v2" 
        - "WUNDERGROUND_KEY_ID=<ADD_YOUR_KEY_ID>"
        - "TWITTER_CONSUMER_KEY=<ADD_YOUR_CONSUMER_KEY>"
        - "TWITTER_CONSUMER_SECRET=<ADD_YOUR_CONSUMER_SECRET>"
```

The `context-provider` container is driven by environment variables as shown:

| Key |Value|Description|
|-----|-----|-----------|
|DEBUG|`proxy:*`| Debug flag used for logging |
|PORT|`3000`|Port used by the content provider proxy and web-app for viewing data |
|CONTEXT_BROKER|`http://orion:1026/v2`| URL of the context broker to  connect to update context|
|WUNDERGROUND_KEY_ID|`<ADD_YOUR_KEY_ID>`| A consumer key used to obtain access to the Weather Underground API|
|TWITTER_CONSUMER_KEY|`<ADD_YOUR_CONSUMER_KEY>`| A consumer key used to obtain access to the Twitter API|
|TWITTER_CONSUMER_SECRET|`<ADD_YOUR_CONSUMER_SECRET>`| A user key used to obtain access to the Twitter API |

The other `context-provider` container configuration values described in the YAML file are not used in this tutorial.


The configuration information for MongoDB and the Orion Context Broker
has been described in a [previous tutorial](https://github.com/Fiware/tutorials.Entity-Relationships/)

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

## Context Provider NGSI proxy

A simple [nodejs](https://nodejs.org/) [Express](https://expressjs.com/) application has been bundled as part of the repository. The application offers an NGSI v1 interface for four different context providers - the Weather Underground API, the Twitter Search API and two dummy data context providers - a static data provider (which always returns the same data) and a random data context provider (which will change every time it is invoked). 

More information about the proxy endpoints can be found [here](https://github.com/Fiware/tutorials.Context-Providers/blob/master/proxy/README.md)

* In order to access the Weather Underground API, you will need to sign up for a key at https://www.wunderground.com/weather/api/ 
* In order to access the Twitter Search API, you will have to create an app in Twitter via  https://apps.twitter.com/app/new to obtain a 
Consumer Key & Consumer Secret. 


Replace the placeholders in `docker-compose.yml` in the root of the repository with the values you obtain for your application:

```yaml
    environment:
        - "DEBUG=proxy:*"
        - "WUNDERGROUND_KEY_ID=<ADD_YOUR_KEY_ID>"
        - "TWITTER_CONSUMER_KEY=<ADD_YOUR_CONSUMER_KEY>"
        - "TWITTER_CONSUMER_SECRET=<ADD_YOUR_CONSUMER_SECRET>"
```

If you do not wish to sign-up for an API key, you can use data from the random data context provider instead.

# Start Up

All services can be initialised from the command line by running the bash script provided within the repository:

```console
./services create; ./services start;
```

This command will also import seed data from the previous [Stock Management example](https://github.com/Fiware/tutorials.CRUD-Operations) on startup.