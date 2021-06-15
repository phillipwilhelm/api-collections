[![FIWARE Core Context Management](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/core.svg)](https://github.com/FIWARE/catalogue/blob/master/core/README.md)
[![NGSI LD](https://img.shields.io/badge/NGSI-linked_data-red.svg)](https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.01.01_60/gs_CIM009v010101p.pdf)

This tutorial teaches FIWARE users how to architect and design a system based on **linked data** and to alter linked
data context programmatically. The tutorial extends the knowledge gained from the equivalent
[NGSI-v2 tutorial](https://github.com/FIWARE/tutorials.Accessing-Context/) and enables a user understand how to write
code in an [NGSI-LD](https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.01.01_60/gs_CIM009v010101p.pdf) capable
[Node.js](https://nodejs.org/) [Express](https://expressjs.com/) application in order to retrieve and alter context
data. This removes the need to use the command-line to invoke cUrl commands.

The tutorial is mainly concerned with discussing code written in Node.js, however some of the results can be checked by
making [cUrl](https://ec.haxx.se/) commands.

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Working-with-Linked-Data/icon/GitHub-Mark-32px.png) [FIWARE 603: Traversing Linked Data Programmatically](https://github.com/Fiware/tutorials.Working-with-Linked-Data)


# Working with Linked Data Entities

> -   “This is the house that Jack built.
> -   This is the malt that lay in the house that Jack built.
> -   This is the rat that ate the malt<br/> That lay in the house that Jack built.
> -   This is the cat<br/> That killed the rat that ate the malt<br/> That lay in the house that Jack built.
> -   This is the dog that chased the cat<br/> That killed the rat that ate the malt<br/> That lay in the house that
>     Jack built.”
>
> ― This Is the House That Jack Built, Traditional English Nursery Rhyme

NSGI-LD is an evolution of NGSI-v2, so it should not be surprising that Smart solutions based on NSGI-LD will need to
cover the same basic scenarios as outlined in the previous NGSI-v2
[tutorial](https://github.com/FIWARE/tutorials.Accessing-Context/) on programatic data access.

NGSI-LD Linked data formalizes the structure of context entities to a greater degree, through restricting data
attributes to be defined as either _Property_ attributes or _Relationship_ attributes only. This means that it is
possible to traverse the context data graph with greater certainty when moving from one _Relationship_ to another. All
the context data entities within the system are defined by JSON-LD data models, which are formally defined by
referencing a context file, and this programatic definition should guarantee that the associated linked entity exists.

Three basic data access scenarios for the supermaket are defined below:

-   Reading Data - e.g. Give me all the data for the **Building** entity `urn:ngsi-ld:Building:store001`
-   Aggregation - e.g. Combine the **Products** entities sold in **Building** `urn:ngsi-ld:Building:store001` and
    display the goods for sale
-   Altering context within the system - e.g. Make a sale of a product:
    -   Update the daily sales records by the price of the **Product**
    -   decrement the `numberOfItems` of the **Shelf** entity
    -   Create a new Transaction Log record showing the sale has occurred
    -   Raise an alert in the warehouse if less than 10 objects remain on sale
    -   etc.

Further advanced scenarios will be covered in later tutorials

## Linked Data Entities within a stock management system

The supermarket data created in the [previous tutorial](https://github.com/FIWARE/tutorials.Relationships-Linked-Data/)
will be loaded into the context broker. The existing relationships between the entities are defined as shown below:

![](https://fiware.github.io/tutorials.Relationships-Linked-Data/img/entities-ld.png)

The **Building**, **Product**, **Shelf** and **StockOrder** entities will be used to display data on the frontend of our
demo application.

## The teaching goal of this tutorial

The aim of this tutorial is to improve developer understanding of programmatic access of context data through defining
and discussing a series of generic code examples covering common data access scenarios. For this purpose a simple
Node.js Express application will be created.

The intention here is not to teach users how to write an application in Express - indeed any language could have been
chosen. It is merely to show how **any** sample programming language could be used alter the context to achieve the
business logic goals.

Obviously, your choice of programming language will depend upon your own business needs - when reading the code below
please keep this in mind and substitute Node.js with your own programming language as appropriate.

# Stock Management Frontend

All the code Node.js Express for the demo can be found within the `ngsi-ld` folder within the GitHub repository.
[Stock Management example](https://github.com/FIWARE/tutorials.Step-by-Step/tree/master/context-provider). The
application runs on the following URLs:

-   `http://localhost:3000/app/store/urn:ngsi-ld:Building:store001`
-   `http://localhost:3000/app/store/urn:ngsi-ld:Building:store002`
-   `http://localhost:3000/app/store/urn:ngsi-ld:Building:store003`
-   `http://localhost:3000/app/store/urn:ngsi-ld:Building:store004`

> :information_source: **Tip** Additionally, you can also watch the status of recent requests yourself by following the
> container logs or viewing information on `localhost:3000/app/monitor` on a web browser.
>
> ![FIWARE Monitor](https://fiware.github.io/tutorials.Accessing-Context/img/monitor.png)

# Prerequisites

## Docker

To keep things simple all components will be run using [Docker](https://www.docker.com). **Docker** is a container
technology which allows to different components isolated into their respective environments.

-   To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A
[YAML file](https://raw.githubusercontent.com/fiware/tutorials.Relationships-Linked-Data/master/docker-compose.yml) is
used configure the required services for the application. This means all container services can be brought up in a
single command. Docker Compose is installed by default as part of Docker for Windows and Docker for Mac, however Linux
users will need to follow the instructions found [here](https://docs.docker.com/compose/install/)

## Cygwin

We will start up our services using a simple bash script. Windows users should download [cygwin](http://www.cygwin.com/)
to provide a command-line functionality similar to a Linux distribution on Windows.

# Architecture

The demo Supermarket application will send and receive NGSI-LD calls to a compliant context broker. Since the NGSI-LD
interface is available on an experimental version of the
[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/), the demo application will only make use of one
FIWARE component.

Currently, the Orion Context Broker relies on open source [MongoDB](https://www.mongodb.com/) technology to keep
persistence of the context data it holds. To request context data from external sources, a simple Context Provider NGSI
proxy has also been added. To visualize and interact with the Context we will add a simple Express application

Therefore, the architecture will consist of three elements:

-   The [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) which will receive requests using
    [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
-   The underlying [MongoDB](https://www.mongodb.com/) database :
    -   Used by the Orion Context Broker to hold context data information such as data entities, subscriptions and
        registrations
-   The **Stock Management Frontend** which will:
    -   Display store information
    -   Show which products can be bought at each store
    -   Allow users to "buy" products and reduce the stock count.

Since all interactions between the elements are initiated by HTTP requests, the entities can be containerized and run
from exposed ports.

![](https://fiware.github.io/tutorials.Accessing-Context/img/architecture.png)

The necessary configuration information for the **Context Provider NGSI proxy** can be seen in the services section the
of the associated `docker-compose.yml` file:

```yaml
tutorial:
    image: fiware/tutorials.context-provider
    hostname: context-provider
    container_name: fiware-tutorial
    networks:
        - default
    expose:
        - "3000"
    ports:
        - "3000:3000"
    environment:
        - "DEBUG=tutorial:*"
        - "WEB_APP_PORT=3000"
        - "NGSI_VERSION=ngsi-ld"
        - "CONTEXT_BROKER=http://orion:1026/ngsi-ld/v1"
```

The `tutorial` container is driven by environment variables as shown:

| Key            | Value                          | Description                                                               |
| -------------- | ------------------------------ | ------------------------------------------------------------------------- |
| DEBUG          | `tutorial:*`                   | Debug flag used for logging                                               |
| WEB_APP_PORT   | `3000`                         | Port used by the Context Provider NGSI proxy and web-app for viewing data |
| CONTEXT_BROKER | `http://orion:1026/ngsi-ld/v1` | URL of the context broker to connect to update context                    |

The other `tutorial` container configuration values described in the YAML file are not used in this section of the
tutorial.

The configuration information for MongoDB and the Orion Context Broker has been described in a
[previous tutorial](https://github.com/FIWARE/tutorials.Relationships-Linked-Data/)

# Start Up

All services can be initialised from the command-line by running the
[services](https://github.com/FIWARE/tutorials.Relationships-Linked-Data/blob/master/services) Bash script provided
within the repository. Please clone the repository and create the necessary images by running the commands as shown:

```bash
git clone https://github.com/FIWARE/tutorials.Working-with-Linked-Data.git
cd tutorials.Working-with-Linked-Data

./services orion
```

> **Note:** If you want to clean up and start over again you can do so with the following command:
>
> ```
> ./services stop
> ```
