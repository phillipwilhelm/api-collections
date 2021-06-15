This tutorial examines the interaction between **NGSI-LD** and **JSON-LD** `@context` files. The `@context` files generated in the [previous tutorial](https://github.com/FIWARE/tutorials.Understanding-At-Context) are used as the underlying data model for inputing context data and context information is queries and read back in different formats.

The `docker-compose` file for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Getting-Started/icon/GitHub-Mark-32px.png) [FIWARE-LD 102: Working with `@context` ](https://github.com/FIWARE/tutorials.Getting-Started/tree/NGSI-LD)

# Working with `@context` files

> “Some quotations are greatly improved by lack of context.”
>
> ― John Wyndham, The Midwich Cuckoos

From the [previous tutorial](https://github.com/FIWARE/tutorials.Understanding-At-Context) we have generated two `@context` files defining the context data entities which will be offered in our simple Smart Farm Management System. This means that we have defined an agreed set of unique IDs (URNs or URLs) for all the
data entities and every single attribute within those entities so that other external applications will be able to programmatically understand the data held within our broker.

For example the attribute `address` is within our smart application is defined as follows:

```jsonld
"@context": {
    "schema": "https://schema.org/",
    "address": "schema:address"
}
```

Which means that every `address` attribute follows the definition as defined by `schema.org`:

`https://schema.org/address` :

![](https://fiware.github.io/tutorials.Working-with-At-Context/img/architecture-ld.png)

A program written by a third party would therefore be able to extract information such the fact an `address` attribute holds a JSON object with a sub-attribute containing the `streetAddress`  by referring to the full [schema.org **JSON-LD** schema](https://schema.org/version/latest/schemaorg-current-http.jsonld)

```jsonld
{
  "@id": "http://schema.org/streetAddress",
  "@type": "rdf:Property",
  "http://schema.org/domainIncludes": {
    "@id": "http://schema.org/PostalAddress"
  },
  "http://schema.org/rangeIncludes": {
    "@id": "http://schema.org/Text"
  },
  "rdfs:comment": "The street address. For example, 1600 Amphitheatre Pkwy.",
  "rdfs:label": "streetAddress"
}
```

This is the **JSON-LD** programmatic syntax allowing computers to extract meaningful data _The attribute `address.streetAddress` is a street_ directly without the need for human intervention.

Imagine the case where a company is contracting agricultural labourers. The farmer will need to be billed for the work done. If such a system is built on JSON-LD, it does not matter if the farmer's Farm Management Information System assigns different names to the attributes of the billing address provided that the farmer and contractor can agree on the well-defined URNS for each attribute as **JSON-LD** can easily translate between the two formats using common expansion and compaction algorithms.

## NGSI-LD Rules

**NGSI-LD** is a formally structured _extended subset_ of **JSON-LD**. Therefore **NGSI-LD** offers all the interoperability and flexibility of **JSON-LD** itself. It also defines its own core `@context` which cannot be overridden for **NGSI-LD** operations. This means that **NGSI-LD** users agree to a common well defined set of rules for structuring their data, and then supplement this with the rest of the **JSON-LD** specification.

Whilst interacting directly with **NGSI-LD** interface of the context broker the additional **NGSI-LD** rules must be respected. However after the data has been extracted it is possible to loosen this requirement and pass the results to third parties as **JSON-LD**.

This tutorial is a simple introduction to the rules and restrictions behind **NGSI-LD** and  will create some **NGSI-LD** entities and then extract the data in different formats. The two main data formats are _normalized_ and _key-value-pairs_. Data returned in the  _normalised_ format respects the **NGSI-LD** rules and may be used directly by another context broker (or any other component offering an **NGSI-LD** interface). Data returned in the  _key-value-pairs_ format is by definition not **NGSI-LD**.

## Content negociation and the `Content-Type` and `Accept` Headers

During content negociation, **NGSI-LD** offers data in one of three formats, these effect the structure of the payload body.

- `Accept: application/json` - the response is in **JSON** format
- `Accept: application/ld+json` - the response is in **JSON-LD** format
- `Accept: application/geo+json` - the response is in **GeoJSON** or **GeoJSON-LD** format

The major difference between **JSON** format and **JSON-LD** format, is that if **JSON-LD** format is chosen, then the `@context` is found as an additional attribute within the body of the response. if the **JSON** only format is used the `@context` is passed as an additional `Link` Header element and is not found in the response body.

Similarly when sending **NGSI-LD** data to the context broker, an application may choose to send a payload including an additional `@context` attribute (in which case `Content-Type: application/ld+json`) or the application may send NGSI-LD data without an additional `@context` attribute (in which case `Content-Type: application/json` and the `Link` header must also be present).

The **GeoJSON** format is only used when querying a context broker for existing data and returns the context in a format suitable for GIS systems. It is a recent addition to the **NGSI-LD** specification and therefore will not be discussed further here.

# Prerequisites

## Docker

To keep things simple all components will be run using [Docker](https://www.docker.com). **Docker** is a container
technology which allows to different components isolated into their respective environments.

-   To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A
[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.Working-with-At-Context/master/docker-compose/orion-ld.yml) is used
configure the required services for the application. This means all container services can be brought up in a single
command. Docker Compose is installed by default as part of Docker for Windows and Docker for Mac, however Linux users
will need to follow the instructions found [here](https://docs.docker.com/compose/install/)

## Cygwin

We will start up our services using a simple bash script. Windows users should download [cygwin](http://www.cygwin.com/)
to provide a command-line functionality similar to a Linux distribution on Windows.
