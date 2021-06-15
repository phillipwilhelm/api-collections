[![FIWARE Security](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/security.svg)](https://www.fiware.org/developers/catalogue/)

This tutorial introduces the administration of level 3 advanced authorization rules into **Keyrock**. The simple verb-resource based permissions are amended to use XACML and new XACML permissions added to the existing roles. The updated ruleset is automatically uploaded to **Authzforce** PDP, so that policy execution points such as the **PEP proxy** are able to apply the latest ruleset.

The tutorial demonstrates examples of interactions using the **Keyrock** GUI, as
well [cUrl](https://ec.haxx.se/) commands used to access the REST
APIs of **Keyrock**  and **Authzforce** 

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Administrating-XACML/icon/GitHub-Mark-32px.png) [FIWARE 406: Administrating XACML](https://github.com/Fiware/tutorials.Administrating-XACML)

# Administrating XACML Rules

> **12.3 Central Terminal Area**
>
> * Red or Yellow Zone
>    * No private vehicle shall stop, wait, or park in the red or yellow zone.
> * White Zone
>    * No vehicle shall stop, wait, or park in the white zone unless actively
> engaged in the immediate loading or unloading of passengers
> and/or baggage.
>
> — Los Angeles International Airport Rules and Regulations, Section 12 - Landside Motor Vehicle Operations

Business rules change over time, and it is necessary to be able to amend access controls accordingly. The [previous tutorial](https://github.com/Fiware/tutorials.XACML-Access-Rules) included a static XACML `<PolicySet>` loaded into **Authzforce**. This component offers advanced authorization (level 3) access control where every policy decision is calculated on the fly and new rules can be applied under new circumstances.
The details of the [Authzforce](https://authzforce-ce-fiware.readthedocs.io/) Policy Decision Point (PDP) were discussed in the [previous tutorial](https://github.com/Fiware/tutorials.XACML-Access-Rules), suffice to say, the **Authzforce** PDP interprets rules according to the
[XACML standard](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=xacml) and offers a means to adjudicate on any access request provided that sufficient information can be supplied.

For full flexibility, it must be possible to load, update and activate a new access control XACML `<PolicySet>` whenever necessary. In order to do, this **Authzforce** offers a simple REST Policy Adminstration Point (PAP), an alternative role-based PAP is available within **Keyrock**

## What is XACML

eXtensible Access Control Markup Language (XACML) is a vendor neutral
declarative access control policy language. It was created to promote common
access control terminology and interoperability. The architectural naming
conventions for elements such as Policy Execution Point (PEP) and Policy
Decision Point (PDP) come from the XACML specifications.

XACML policies are split into a hierarchy of three levels - `<PolicySet>`,
`<Policy>` and `<Rule>`, the `<PolicySet>` is a collection of `<Policy>`
elements each of which contain one or more `<Rule>` elements.

Each `<Rule>` within a `<Policy>` is evaluated as to whether it should grant
access to a resource - the overall `<Policy>` result is defined by the overall
result of all `<Rule>` elements processed in turn. Separate `<Policy>` results
are then evaluated against each other using combining alogorthms define which
`<Policy>` wins in case of conflict.

Further information can be found within the [XACML standard](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=xacml)

## PAP - Policy Administration Point

For the first half of the tutorial, a simple two rule `<PolicySet>` will be administered using the **Authzforce** PAP. Thereafter the **Keyrock** GUI will be used to administer XACML rules within the existing tutorial application  on an individual XACML `<Rule>` level. The policy decision request code within the **PEP-Proxy** may also need to be customized to enable the enforcement of complex XACML rules.

### Authzforce PAP

Within the **Authzforce** PAP all CRUD actions occur on the `<PolicySet>` level. It is therefore necessary to create a complete, valid XACML file before uploading it to the service. There is no GUI available to ensure the validity of the  `<PolicySet>` prior to uploading the XACML.

### Keyrock PAP

**Keyrock** can create a valid XACML file based on available roles and permissions and pass this to **Authzforce**. Indeed **Keyrock** already does this whenever it combines with **Authzforce** as all its own basic authorization (level 2) permissions must be translated into advanced authorization (level 3) permissions before they can be adjudicated by **Authzforce**.

Within **Keyrock**, each role corresponds to an XACML `<Policy>`, each permission within that role corresponds to an XACML `<Rule>`. There is a GUI available for uploading and amending the XACML for each `<Rule>` and all CRUD actions occur on the `<Rule>` level.

Provided care is taken when creating `<Rule>` you can use **Keyrock** to simplify the administration of XACML and create a valid `<PolicySet>` for **Authzforce**.

## PEP - Policy Execution Point

When using advanced authorization (level 3),  a policy execution point sends the an authorization request to he relevant domain endpoint within **Authzforce**,
providing all of the information necessary for **Authzforce** to provide a
judgement. Details of the interaction can be found in the [previous tutorial](https://github.com/Fiware/tutorials.XACML-Access-Rules).

The full code to supply each request to **Authzforce** can be found within the
tutorials'
[Git Repository](https://github.com/Fiware/tutorials.Step-by-Step/blob/master/context-provider/lib/azf.js)

Obviously the definition of _"all of the information necessary"_ may change
over time, applications must therefore be flexible enough to be able to modify the requests sent to ensure that sufficient information is passed.

# Prerequisites

## Docker

To keep things simple all components will be run using
[Docker](https://www.docker.com). **Docker** is a container technology which
allows to different components isolated into their respective environments.

-   To install Docker on Windows follow the instructions
    [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions
    [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions
    [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker
applications. A
[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.Identity-Management/master/docker-compose.yml)
is used configure the required services for the application. This means all
container services can be brought up in a single command. Docker Compose is
installed by default as part of Docker for Windows and Docker for Mac, however
Linux users will need to follow the instructions found
[here](https://docs.docker.com/compose/install/)

## Cygwin

We will start up our services using a simple bash script. Windows users should
download [cygwin](http://www.cygwin.com/) to provide a command-line
functionality similar to a Linux distribution on Windows.

# Architecture

This application adds OAuth2-driven security into the existing Stock Management
and Sensors-based application created in
[previous tutorials](https://github.com/Fiware/tutorials.IoT-Agent/) by using
the data created in the first
[security tutorial](https://github.com/Fiware/tutorials.Identity-Management/)
and reading it programmatically. It will make use of three FIWARE components -
the [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/),the
[IoT Agent for UltraLight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/)
and integrates the use of the
[Keyrock](https://fiware-idm.readthedocs.io/en/latest/) Generic enabler. Usage
of the Orion Context Broker is sufficient for an application to qualify as
_“Powered by FIWARE”_.

Both the Orion Context Broker and the IoT Agent rely on open source
[MongoDB](https://www.mongodb.com/) technology to keep persistence of the
information they hold. We will also be using the dummy IoT devices created in
the [previous tutorial](https://github.com/Fiware/tutorials.IoT-Sensors/).
**Keyrock** uses its own [MySQL](https://www.mysql.com/) database.

Therefore the overall architecture will consist of the following elements:

-   The FIWARE
    [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) which
    will receive requests using
    [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
-   The FIWARE
    [IoT Agent for UltraLight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/)
    which will receive southbound requests using
    [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) and convert
    them to
    [UltraLight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
    commands for the devices
-   FIWARE [Keyrock](https://fiware-idm.readthedocs.io/en/latest/) offer a
    complement Identity Management System including:
    -   An OAuth2 authentication system for Applications and Users
    -   A site graphical frontend for Identity Management Administration
    -   An equivalent REST API for Identity Management via HTTP requests

-   FIWARE [Authzforce](https://fiware-pep-proxy.rtfd.io/) is a XACML Server providing an interpretive Policy Decision Point (PDP)
    access to the **Orion** and/or **IoT Agent** microservices
-   FIWARE [Wilma](https://fiware-pep-proxy.rtfd.io/) is a PEP Proxy securing
    access to the **Orion** microservices, it requests authorisation decisions from **Authzforce**
-   The underlying [MongoDB](https://www.mongodb.com/) database :
    -   Used by the **Orion Context Broker** to hold context data information
        such as data entities, subscriptions and registrations
    -   Used by the **IoT Agent** to hold device information such as device URLs
        and Keys
-   A [MySQL](https://www.mysql.com/) database :
    -   Used to persist user identities, applications, roles and permissions
-   The **Stock Management Frontend** does the following:
    -   Displays store information
    -   Shows which products can be bought at each store
    -   Allows users to "buy" products and reduce the stock count.
    -   Allows authorized users into restricted areas, it requests authoriation decisions from **Authzforce**
-   A webserver acting as set of
    [dummy IoT devices](https://github.com/Fiware/tutorials.IoT-Sensors) using
    the
    [UltraLight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
    protocol running over HTTP - access to certain resources is restricted.

Since all interactions between the elements are initiated by HTTP requests, the
entities can be containerized and run from exposed ports.

![](https://fiware.github.io/tutorials.Administrating-XACML/img/architecture.png)


The all container configuration values described in the YAML file
have been described in previous tutorials



# Start Up

To start the installation, do the following:

```console
git clone git@github.com:Fiware/tutorials.Administrating-XACML.git
cd tutorials.Administrating-XACML

./services create
```

> **Note** The initial creation of Docker images can take up to three minutes

Thereafter, all services can be initialized from the command-line by running the
[services](https://github.com/Fiware/tutorials.Administrating-XACML/blob/master/services)
Bash script provided within the repository:

```console
./services start
```


> **Note:** If you want to clean up and start over again
> you can do so with the following command:
>
> ```
> ./services stop
> ```

### Dramatis Personae

The following people at `test.com` legitimately have accounts within the
Application

-   Alice, she will be the Administrator of the **Keyrock** Application
-   Bob, the Regional Manager of the supermarket chain - he has several store
    managers under him:
    -   Manager1
    -   Manager2
-   Charlie, the Head of Security of the supermarket chain - he has several
    store detectives under him:
    -   Detective1
    -   Detective2

| Name       | eMail                     | Password |
| ---------- | ------------------------- | -------- |
| alice      | alice-the-admin@test.com  | `test`   |
| bob        | bob-the-manager@test.com  | `test`   |
| charlie    | charlie-security@test.com | `test`   |
| manager1   | manager1@test.com         | `test`   |
| manager2   | manager2@test.com         | `test`   |
| detective1 | detective1@test.com       | `test`   |
| detective2 | detective2@test.com       | `test`   |

The following people at `example.com` have signed up for accounts, but have no
reason to be granted access

-   Eve - Eve the Eavesdropper
-   Mallory - Mallory the malicious attacker
-   Rob - Rob the Robber

| Name    | eMail               | Password |
| ------- | ------------------- | -------- |
| eve     | eve@example.com     | `test`   |
| mallory | mallory@example.com | `test`   |
| rob     | rob@example.com     | `test`   |


# XACML Administration

To apply an access control policy, it is necessary to be able to do the following:

a) Create a consistent `<PolicySet>`
b) Supply a Policy Execution Point (PEP) which provides necessary data

As will be seen, **Keyrock** is able help with the first point, and custom code within the **PEP Proxy** can help with the second. **Authzforce** itself does not offer a UI, and is not concerned with generation and management of XACML policies - it assumes that each `<PolicySet>` it receives has already been generated by another component.

Full-blown XACML editors are available, but the limited editor within **Keyrock** is usually sufficient for most access control scenarios.