This tutorial introduces linked data concepts to the FIWARE Platform. The supermarket chain’s store finder application
is recreated using **NGSI-LD** the differences between the **NSGI v2** and **NGSI-LD** interfaces are highlighted and
discussed. The tutorial is a direct analogue of the original getting started tutorial but uses API calls from the
**NGSI-LD** interface.

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Linked-Data/icon/GitHub-Mark-32px.png) [FIWARE 601: Linked Data](https://github.com/Fiware/tutorials.Linked-Data)


# Adding Linked Data concepts to FIWARE Data Entities.

> “Six degrees of separation doesn't mean that everyone is linked to everyone else in just six steps. It means that a
> very small number of people are linked to everyone else in a few steps, and the rest of us are linked to the world
> through those special few.”
>
> ― Malcolm Gladwell, The Tipping Point

The introduction to FIWARE [Getting Started tutorial](https://github.com/FIWARE/tutorials.Getting-Started) introduced
the [NSGI v2](https://fiware.github.io/specifications/OpenAPI/ngsiv2) interface that is commonly used to create and
manipulate context data entities. An evolution of that interface has created a supplementary specification called
[NGSI-LD](https://forge.etsi.org/swagger/ui/?url=https://forge.etsi.org/gitlab/NGSI-LD/NGSI-LD/raw/master/spec/updated/full_api.json)
as a mechanism to enhance context data entities though adding the concept of **linked data**. This tutorial will
introduce the background of the ideas behind the new interface and compare and contrast how to create and manipulate
data entites as linked data.

Addtional tutorials in the series will further discuss data relationships an how to create context data entities using
linked data enabling the full knowledge graph to be traversed.

## What is Linked Data?

All users of the Internet will be familiar with the concept of hypertext links, the way that a link on one web page is
able to guide the browser to loading another page from a known location.

Whilst humans are able to understand relationship discoverability and how links work, computers find this much more
difficult, and require a well-defined protocol to be able to traverse from one data element to another held in a
separate location.

Creating a system of readable links for computers requires the use of a well defined data format
([JSON-LD](http://json-ld.org/)) and assignation of unique IDs
([URLs or URNs](https://stackoverflow.com/questions/4913343/what-is-the-difference-between-uri-url-and-urn)) for both
data entities and the relationships between entities so that semantic meaning can be programmatically retrieved from the
data itself.

Properly defined linked data can be used to help answer big data questions, and the data relationships can be traversed
to answer questions like _"Which products are currently avaiable on the shelves of Store X and what prices are they sold
at?"_

### Video: What is Linked Data?

[![](http://img.youtube.com/vi/4x_xzT5eF5Q/0.jpg)](https://www.youtube.com/watch?v=4x_xzT5eF5Q "Introduction")

Click on the image above to watch an introductory video on linked data concepts

JSON-LD is an extension of JSON , it is a standard way of avoiding ambiguity when expressing linked data in JSON so that
the data is structured in a format which is parsable by machines. It is a method of ensuring that all data attributes
can be easily compared when coming from a multitude of separate data sources, which could have a different idea as to
what each attribute means. For example, when two data entities have a `name` attribute how can the computer be certain
that is refers to a _"Name of a thing"_ in the same sense (rather than a **Username** or a **Surname** or something).
URLs and datamodels are used to remove ambiguity by allowing attributes to have a both short form (such as `name`) and a
fully specified long form (such `http://schema.org/name`) which means it is easy to discover which attribute have a
common meaning within a data structure.

JSON-LD introduces the concept of the `@context` element which provides additional information allowing the computer to
interpret the rest of the data with more clarity and depth.

Furthermore the JSON-LD specification enables you to define a unique `@type` associating a well-defined
[data model](https://fiware-datamodels.readthedocs.io/en/latest/guidelines/index.html) to the data itself.

### Video: What is JSON-LD?

[![](http://img.youtube.com/vi/vioCbTo3C-4/0.jpg)](https://www.youtube.com/watch?v=vioCbTo3C-4 "JSON-LD")

Click on the image above to watch a video describing the basic concepts behind JSON-LD.

## What is NGSI-LD?

**NGSI-LD** is an evolution of the **NGSI v2** information model, which has been modified to improve support for linked
data (entity relationships), property graphs and semantics (exploiting the capabilities offered by JSON-LD). This work
has been conducted under the ETSI ISG CIM initiative and the updated specification hhas been branded as
[NGSI-LD](https://www.etsi.org/deliver/etsi_gs/CIM/001_099/009/01.01.01_60/gs_CIM009v010101p.pdf). The main constructs
of NGSI-LD are: _Entity_, _Property_ and _Relationship_. NGSI-LD Entities (instances) can be the subject of Properties
or Relationships. In terms of the traditional NGSI v2 data model, Properties can be seen as the combination of an
attribute and its value. Relationships allow to establish associations between instances using linked data.

### NGSI v2 Data Model

As a reminder, the NGSI v2 data model is quite simple. It can be summarized as shown below:

![](https://fiware.github.io/tutorials.Linked-Data/img/ngsi-v2.png)

The core element of NGSI v2 is the data _entity_, typically a real object with a changing state (such as a **Store**, a
**Shelf** and so on). Entities have _attributes_ (such as `name` and `location`) and these in turn hold _metadata_ such
as `accuracy` - i.e. the accuracy of a `location` reading.

Every _entity_ must have a `type` which defines the sort of thing the entity describes, but giving an NGSI v2 entity the
`type=Store` is relatively meaningless as no-one is obliged to shape their own **Store** entities in the same fashion.
Similarly adding an attribute called `name` doesn't suddenly make it hold the same data as someone else's `name`
attribute.

Relationships can be defined using NGSI v2, but only so far as giving the attribute an appropriate attribute name
defined by convention ( e.g. starting with `ref`, such as `refManagedBy`) and assigning the attribute
`type=Relationship` which again is purely a naming convention with no real semantic weight.

### NGSI LD Data Model

The NGSI LD data model is more complex, with more rigid definitions of use which lead to a navigable knowledge graph.

![](https://fiware.github.io/tutorials.Linked-Data/img/ngsi-ld.png)

Once again, _entity_ can be considered to be the core element. Every entity must use a unique `id`
[URN](https://en.wikipedia.org/wiki/Uniform_resource_name), there is also a `type`, used to define the structure of the
data held, which is also a URN. This URN should correspond to a well-defined data model which can be found on the web.
For example the URN `https://uri.fiware.org/ns/datamodels/Building` is used to define common data model for a
[Building](https://fiware-datamodels.readthedocs.io/en/latest/Building/Building/doc/spec/index.html).

_Entities_ can have _properties_ and _relationships_. Ideally the name of each _property_ should also be a well defined
URN which corresponds to a common concept found across the web (e.g. `http://schema.org/address` is a common URN for the
physical address of an item). The _property_ will also have a value which will reflect the state of that property (e.g
`name="Checkpoint Markt"`). Finally a property may itself have further properties (a.k.a. _properties-of-properties_)
which reflect further information about the property itself. Properties and relationships may in turn have a linked
embedded structure (of _properties-of-properties_ or _properties-of-relationships or relationships-of-properties_ or
_relationships-of-relationships_ etc.) which lead to the following:

An NGSI LD Data Entity (e.g. a supermarket):

-   Has an `id` which must be unique. For example `urn:ngsi-ld:Building:store001`,
-   Has `type` which should be a fully qualified URN of a well defined data model. For example
    `https://uri.fiware.org/ns/datamodels#Building`
-   Has _property_ of the entity, for example, an `address` attribute which holds the adress of the store. This can be
    expanded into `http://schema.org/address`, which is known as a fully qualified name
    ([FQN](https://en.wikipedia.org/wiki/Fully_qualified_name)).
-   The `address`, like any _property_ will have a _value_ corresponding to the _property_ `address` (e.g. _Bornholmer
    Straße 65, 10439 Prenzlauer Berg, Berlin_
-   Has a _property-of-a-property_ of the entity, for example a `verified` field for the `address`.
-   Has a _relationship_ of the entity, for example, a `managedBy` field where the relationship `managedBy` corresponds
    to another data entity : `urn:ngsi-ld:Person:bob-the-manager`
-   The relationship `managedBy`, may itself have a _property-of-a-relationship_ (e.g. `since`), this holds the date Bob
    started working the store
-   The relationship `managedBy`, may itself have a _relationship-of-a-relationship_ (e.g. `subordinateTo`), this holds
    the URN of the area manager above Bob in the hierarchy.

As you can see the knowledge graph is well defined and can be expanded indefinitely.

Relationships will be dealt with in more detail in a subsequent tutorial.

# Prerequisites

## Docker

To keep things simple all components will be run using [Docker](https://www.docker.com). **Docker** is a container
technology which allows to different components isolated into their respective environments.

-   To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A
[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.Identity-Management/master/docker-compose.yml) is used
configure the required services for the application. This means all container services can be brought up in a single
command. Docker Compose is installed by default as part of Docker for Windows and Docker for Mac, however Linux users
will need to follow the instructions found [here](https://docs.docker.com/compose/install/)

## Cygwin

We will start up our services using a simple bash script. Windows users should download [cygwin](http://www.cygwin.com/)
to provide a command-line functionality similar to a Linux distribution on Windows.

