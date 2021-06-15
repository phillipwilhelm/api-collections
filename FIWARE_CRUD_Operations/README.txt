This tutorial builds on the data created in the previous [stock management example](http://fiware.github.io/tutorials.Entity-Relationships/) and introduces the concept of [CRUD operations](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete), allowing users to manipulate the data held within the context.

The `docker-compose` file for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.CRUD-Operations/icon/GitHub-Mark-32px.png) [FIWARE 103: Manipulating Context Data through CRUD Operations ](https://github.com/Fiware/tutorials.CRUD-Operations)

# Data Entities

Within the FIWARE platform, an entity represents the state of a physical or
conceptual object which exists in the real world.

## Entities within a stock management system

Within our simple stock management system, we currently have four entity types.
The relationships between our entities are defined as shown below:

![](https://fiware.github.io/tutorials.Entity-Relationships/img/entities.png)

-   A **Store** is a real world bricks and mortar building. Stores would have
    properties such as:
    -   Store name, e.g. "Checkpoint Markt"
    -   Address, e.g. "Friedrichstraße 44, 10969 Kreuzberg, Berlin"
    -   Physical location, e.g. _52.5075 N, 13.3903 E_
-   A **Shelf** is a real world object to hold items which we wish to sell.
    Each shelf would have properties such as:
    -   Shelf name, e.g. "Wall Unit"
    -   Physical location, e.g. _52.5075 N, 13.3903 E_
    -   Maximum capacity
    -   An association to the store in which the shelf is located
-   A **Product** is defined as something that we sell - it is a conceptual
    object. Products would have properties such as:
    -   Product name, e.g. "Vodka"
    -   Price, e.g. 13.99 Euros
    -   Size, e.g. Small
-   An **Inventory Item** is another conceptual entity, used to associate
    products, stores, shelves and physical objects. It would have properties
    such as:
    -   An association to the product being sold
    -   An association to the store in which the product is being sold
    -   An association to the shelf where the product is being displayed
    -   Stock count, i.e. product quantity available in the warehouse
    -   Shelf count, i.e. number of items available on the shelf

As you can see, each of the entities defined above contain some properties which
are liable to change. For example, product price could change, stock could be sold
and the number of items on the shelves would drop.

# Architecture

This application will only make use of one FIWARE component - the
[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/). Using
the Orion Context Broker is sufficient for an application to qualify as
_“Powered by FIWARE”_.

Currently, the Orion Context Broker relies on open source
[MongoDB](https://www.mongodb.com/) technology to store the context data it
manages. Therefore, the architecture will consist of two components:

-   The [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/)
    which will receive requests using
    [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
-   The underlying [MongoDB](https://www.mongodb.com/) database:
    -   Used by the Orion Context Broker to store context information such
        as data entities, subscriptions and registrations

Since the two components interact by means of HTTP requests, they can be
containerized and run from exposed ports.

![](https://fiware.github.io/tutorials.CRUD-Operations/img/architecture.png)

The necessary configuration information can be seen in the services section of
the associated `docker-compose.yml` file:

```yaml
orion:
    image: fiware/orion:latest
    hostname: orion
    container_name: orion
    depends_on:
        - mongo-db
    networks:
        - default
    expose:
        - "1026"
    ports:
        - "1026:1026"
    command: -dbhost mongo-db -logLevel DEBUG
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
    command: --bind_ip_all --smallfiles
```

Both containers reside on the same network - the Orion Context Broker is
listening on port `1026` and MongoDB is listening on the default port `271071`.
For the sake of this tutorial, we have also made the two ports available from
outside the network so that cUrl or Postman can access them without having to
be run from inside the network. The command-line initialization should be self
explanatory.

# Prerequisites

## Docker

To keep things simple both components will be run using
[Docker](https://www.docker.com). **Docker** is a container technology which
allows to package each component with its environment and run it in isolation.

-   To install Docker on Windows follow the instructions
    [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions
    [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions
    [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker
applications. A
[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.Entity-Relationships/master/docker-compose.yml)
is used configure the required services for the application. This means all
container services can be brought up with a single command. Docker Compose is
installed by default as part of Docker for Windows and Docker for Mac, however
Linux users will need to follow the instructions found
[here](https://docs.docker.com/compose/install/)

You can check your current **Docker** and **Docker Compose** versions using the
following commands:

```console
docker-compose -v
docker version
```

Please ensure that you are using Docker version 18.03 or higher and Docker
Compose 1.21 or higher and upgrade if necessary.

## Cygwin

We will start up our services using a simple bash script. Windows users should
download [cygwin](http://www.cygwin.com/) to provide a command-line
functionality similar to a Linux distribution on Windows.

# Start Up

All services can be initialised from the command-line by running the bash script
provided within the repository. Please clone the repository and create the
necessary images by running the commands as shown below:

```console
git clone git@github.com:Fiware/tutorials.CRUD-Operations.git
cd tutorials.CRUD-Operations

./services start
```

This command will also import seed data from the previous
[Store Finder tutorial](https://github.com/Fiware/tutorials.Entity-Relationships)
on startup.

> :information_source: **Note:** If you want to clean up and start over again
> you can do so with the following command:
>
> ```console
> ./services stop
> ```

# What is CRUD?

**Create**, **Read**, **Update** and **Delete** are the four basic functions of
persistent storage. These operations are usually referred to using the acronym
**CRUD**. Within a database each of these operations map directly to a series of
commands, however their relationship with a RESTful API is slightly more complex.

The [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) uses
[NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) to manipulate the
context data. As a RESTful API, requests to manipulate the data held within the
context follow the standard conventions found when mapping HTTP verbs to CRUD
operations.

## Entity CRUD Operations

For operations where the `<entity-id>` is not yet known within the context, or
is unspecified, the `/v2/entities` endpoint is used.

Once an `<entity-id>` is known within the context, individual data entities can
be manipulated using the `/v2/entities/<entity-id>` endpoint.

It is recommended that entity identifiers should be URNs following the
[NGSI-LD guidelines](https://docbox.etsi.org/ISG/CIM/Open/ISG_CIM_NGSI-LD_API_Draft_for_public_review.pdf),
therefore each `id` is a URN which follows a standard format:
`urn:ngsi-ld:<entity-type>:<entity-id>`. This helps making every `id` in the
context data unique.

| HTTP Verb  |                                               `/v2/entities`                                               |                                              `/v2/entities/<entity-id>`                                              |
| ---------- | :--------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------: |
| **POST**   |                                CREATE a new entity and add to the context.                                 |                                 CREATE or UPDATE an attribute of a specified entity.                                 |
| **GET**    | READ entity data from the context. This will return data from multiple entities. The data can be filtered. | READ entity data from a specified entity. This will return data from a single entity only. The data can be filtered. |
| **PUT**    |                                                    :x:                                                     |                                                         :x:                                                          |
| **PATCH**  |                                                    :x:                                                     |                                                         :x:                                                          |
| **DELETE** |                                                    :x:                                                     |                                          DELETE an entity from the context                                           |

A complete list of entity endpoints can be found in the
[NGSI v2 Swagger Specification](https://fiware.github.io/specifications/OpenAPI/ngsiv2#/Entities)

## Attribute CRUD Operations

To perform CRUD operations on attributes, the `<entity-id>` must be known. Each
attribute is effectively a key-value pair.

There are three endpoints:

-   `/v2/entities/<entity-id>/attrs` is only used for a patch operation to
    update one or more exisiting attributes.
-   `/v2/entities/<entity-id>/attrs/<attribute>` is used to manipulate an
    attribute as a whole.
-   `/v2/entities/<entity-id>/attrs/<attribute>/value` is used to read or update
    the `value` of an attribute, leaving the `type` untouched.

| HTTP Verb   |                           `.../attrs`                           |                `.../attrs/<attribute>`                |                              `.../attrs/<attribute>/value`                               |
| ----------- | :-------------------------------------------------------------: | :---------------------------------------------------: | :--------------------------------------------------------------------------------------: |
| **POST**    |                               :x:                               |                          :x:                          |                                           :x:                                            |
| **GET**     |                               :x:                               |                          :x:                          | READ the value of an attribute from a specified entity. This will return a single field. |
| **PUT**     |                               :x:                               |                          :x:                          |              UPDATE the value of single attribute from a specified entity.               |
| **PATCH**   | UPDATE one or more existing attributes from an existing entity. |                          :x:                          |                                           :x:                                            |
| **DELETE**. |                               :x:                               | DELETE an existing attribute from an existing entity. |                                           :x:                                            |

A complete list of attribute endpoints can be found in the
[NGSI v2 Swagger Specification](https://fiware.github.io/specifications/OpenAPI/ngsiv2#/Attributes)

## Batch CRUD Operations

Additionally the Orion Context Broker has a convenience batch operation endpoint
`/v2/op/update` to manipulate multiple entities in a single operation.

Batch operations are always triggered by a POST request where the payload is an
object with two properties:

-   `actionType` specifies the kind of action to invoke (e.g. `delete`)
-   `entities` is an array of objects holding the list of entities to update, along
    with the relevant entity data used to perform the operation.
