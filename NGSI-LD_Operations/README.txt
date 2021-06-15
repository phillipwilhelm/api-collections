This tutorial teaches **NGSI-LD** users about CRUD Operations. The tutorial outlines example usage of the various ways
of amending context as detailed within the
[NGSI-LD specification](https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.03.01_60/gs_cim009v010301p.pdf). A
series of entities representing temperature sensors are created, modified and deleted based on the temperature sensor
model defined in an [earlier tutorial](https://github.com/FIWARE/tutorials.Understanding-At-Context).

The `docker-compose` file for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.CRUD-Operations/icon/GitHub-Mark-32px.png) [FIWARE-LD 103: Manipulating Context Data through CRUD Operations ](https://github.com/FIWARE/tutorials.CRUD-Operations)

# NGSI-LD CRUD Operations

> “Ninety-percent of everything is crud.”
>
> ― Theodore Sturgeon, Venture Science Fiction Magazine

**CRUD** Operations (**Create**, **Read**, **Update** and **Delete**) are the four basic functions of persistent
storage. For a smart system based on **NGSI-LD**, **CRUD** actions allow the developer to manipulate the context data
within the system. Every **CRUD** operation is clearly defined within the
[NGSI-LD specification](https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.03.01_60/gs_cim009v010301p.pdf), so all
NGSI-LD compliant context brokers offer the same interface with the same NGSI-LD operations.

This tutorial will describe the rational behind each operation, when to use it and how to execute the various **CRUD**
operations. Since **NGSI-LD** is based on **JSON-LD** passing of `@context` as part of each request in mandatory. For
**CRUD** operations this is typically passed as a `Link` header, although as we have seen is also possible to pass an
`@context` attribute as part of the body of the request if `Content-Type: application/ld+json`. However for GET
requests, the `@context` cannot be placed in the payload body technique as GET requests have no body.

## Context Entity CRUD Operations

There are four endpoints used for CRUD operations on an individual data entity. These follow the usual rules for
hierarchical entities within RESTful applications.

For operations where the `<entity-id>` is not yet known within the context, or is unspecified, the
`/ngsi-ld/v1/entities` endpoint is used. As an example, this is used for creating new entities.

Once an `<entity-id>` is known within the context, individual data entities can be manipulated using the
`/ngsi-ld/v1/entities/<entity-id>` endpoint.

General Attribute operations on a known entity occur on the `/ngsi-ld/v1/entities/<entity-id>/attrs` endpoint and
operations on individual attributes occur on the `/ngsi-ld/v1/entities/<entity-id>/attrs/<attr-id>`.

When requesting data or modifying individual entities, the various CRUD operations map naturally to HTTP verbs.

-   **GET** - for reading data
-   **POST** - for creating new entities and attributes
-   **PATCH** - for amending entities and attributes
-   **DELETE** - for deleting entities and attributes

## Context Entity Batch Operations

Batch operations allow users to modify multiple data entities with a single request. All batch operations are mapped to
the **POST** HTTP verb.

-   `/entityOperations/create`
-   `/entityOperations/update`
-   `/entityOperations/upsert`
-   `/entityOperations/delete`

# Prerequisites

## Docker

To keep things simple all components will be run using [Docker](https://www.docker.com). **Docker** is a container
technology which allows to different components isolated into their respective environments.

-   To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A
[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.CRUD-Operations/NGSI-LD/docker-compose/orion-ld.yml) is
used configure the required services for the application. This means all container services can be brought up in a
single command. Docker Compose is installed by default as part of Docker for Windows and Docker for Mac, however Linux
users will need to follow the instructions found [here](https://docs.docker.com/compose/install/)

## Cygwin

We will start up our services using a simple bash script. Windows users should download [cygwin](http://www.cygwin.com/)
to provide a command-line functionality similar to a Linux distribution on Windows.

# Architecture

The demo application will send and receive NGSI-LD calls to a compliant context broker. Since the standardized NGSI-LD
interface is available across multiple context brokers, so we only need to pick one - for example the
[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/). The application will therefore only make use of
one FIWARE component.

Currently, the Orion Context Broker relies on open source [MongoDB](https://www.mongodb.com/) technology to keep
persistence of the context data it holds.

To promote interoperability of data exchange, NGSI-LD context brokers explicitly expose a
[JSON-LD `@context` file](https://json-ld.org/spec/latest/json-ld/#the-context) to define the data held within the
context entities. This defines a unique URI for every entity type and every attribute so that other services outside of
the NGSI domain are able to pick and choose the names of their data structures. Every `@context` file must be available
on the network. In our case the tutorial application will be used to host a series of static files.

Therefore, the architecture will consist of three elements:

-   The [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) which will receive requests using
    [NGSI-LD](https://forge.etsi.org/swagger/ui/?url=https://forge.etsi.org/gitlab/NGSI-LD/NGSI-LD/raw/master/spec/updated/full_api.json)
-   The underlying [MongoDB](https://www.mongodb.com/) database :
    -   Used by the Orion Context Broker to hold context data information such as data entities, subscriptions and
        registrations
-   The **Tutorial Application** does the following:
    -   Offers static `@context` files defining the context entities within the system.

Since all interactions between the three elements are initiated by HTTP requests, the elements can be containerized and
run from exposed ports.

![](https://fiware.github.io/tutorials.CRUD-Operations/img/architecture-ld.png)

The necessary configuration information can be seen in the services section of the associated `orion-ld.yml` file:

```yaml
orion:
    image: fiware/orion-ld
    hostname: orion
    container_name: fiware-orion
    depends_on:
        - mongo-db
    networks:
        - default
    ports:
        - "1026:1026"
    command: -dbhost mongo-db -logLevel DEBUG
    healthcheck:
        test: curl --fail -s http://orion:1026/version || exit 1
```

```yaml
mongo-db:
    image: mongo:3.6
    hostname: mongo-db
    container_name: db-mongo
    expose:
        - "27017"
    ports:
        - "27017:27017"
    networks:
        - default
    command: --nojournal
```

```yaml
tutorial:
    image: fiware/tutorials.ngsi-ld
    hostname: tutorial
    container_name: fiware-tutorial
    networks:
        default:
            aliases:
                - context
    expose:
        - 3000
```

The necessary configuration information can be seen in the services section of the associated `docker-compose.yml` file.
It has been described in a [previous tutorial](https://github.com/FIWARE/tutorials.Working-with-At-Context/)

# Start Up

All services can be initialised from the command-line by running the
[services](https://github.com/FIWARE/tutorials.NGSI-LD-Operations/blob/master/services) Bash script provided within the
repository. Please clone the repository and create the necessary images by running the commands as shown:

```bash
git clone https://github.com/FIWARE/tutorials.NGSI-LD-Operations.git
cd tutorials.NGSI-LD-Operations

./services orion|scorpio
```

> **Note:** If you want to clean up and start over again you can do so with the following command:
>
> ```
> ./services stop
> ```