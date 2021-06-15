This tutorial is an introduction to [FIWARE Cygnus](http://fiware-cygnus.readthedocs.io/en/latest/) - a generic enabler which is used to persist context data into third-party databases creating a historical view of the context. The tutorial activates the IoT sensors connected in the [previous tutorial](https://github.com/Fiware/tutorials.IoT-Agent) and persists measurements
from those sensors into a database for further analysis.

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Historic-Context-Flume/icon/GitHub-Mark-32px.png) [FIWARE 301: Persisting Context Data](https://github.com/Fiware/tutorials.Historic-Context-Flume)

# Data Persistence

> "History will be kind to me for I intend to write it."
>
> — Winston Churchill


Previous tutorials have introduced a set of IoT Sensors (providing measurements of the
state of the real world), and two FIWARE Components - the **Orion Context Broker** and an **IoT Agent**. 
This tutorial will introduct a new data persistance component - FIWARE **Cygnus**.

The system so far has been built up to handle the current context, in other words it holds the data entities
defining the state of the real-world objects at a given moment in time.

From this definition you can see - context is only interested in the **current** state of the system
It is not the responsibility of any of the existing components to report on the historical state of the system,
the context is based on the last measurement each sensor has sent data to the context broker.

In order to do this, we will need to extend the existing architecture to persist changes of state into a database whenever 
the context is updated.

Persisting historical context data is useful for big data analysis - it can be used to discover trends, or data 
can be sampled and aggregated to remove the influence of outlying data measurements. However within each Smart Solution,
the significance of each entity type will differ and entities and attributes may need to be sampled at different rates.

Since the business requirements for using context data differ from application to appliation, there is no one standard use 
case  for historical data persistence - each situation is unique - it is not the case that one size fits all.
Therefore rather than overloading the context broker with the job of historical context data persistence, this role has been
separated out into a separate, highly configurable component - **Cygnus**.

As you would expect, **Cygnus**, as part of an Open Source platform, is technology agnostic regarding the database 
to be used for data persistance. The database you choose to use will depend upon your own business needs. 

However there is a cost to offering this flexibility - each part of the system must be separately configured and
notifications must be set up to only pass the minimal data required as necessary.




#### Device Monitor

For the purpose of this tutorial, a series of dummy IoT devices have been created, which will be attached to the context broker.
The state of each device can be seen on the UltraLight device monitor web-page found at: `http://localhost:3000/device/monitor`

![FIWARE Monitor](https://fiware.github.io/tutorials.Historic-Context-Flume/img/device-monitor.png)




# Architecture

This application builds on the components and dummy IoT devices created in 
[previous tutorials](https://github.com/Fiware/tutorials.IoT-Agent/). It will make use of three FIWARE components - 
the [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/), the
[IoT Agent for UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/) and introduce the
[Cygnus Generic Enabler](http://fiware-cygnus.readthedocs.io/en/latest/) for persisting context data to a database.
Additional databases are now involved - both the Orion Context Broker and the IoT Agent rely on [MongoDB](https://www.mongodb.com/) technology to keep persistence of the information they hold, and we will be persisting our historical context data another database - either **MySQL** , **PostgreSQL**  or **Mongo-DB** database.


Therefore the overall architecture will consist of the following elements:

* Three **FIWARE Generic Enablers**:
  * The FIWARE [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) which will receive requests using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
  * The FIWARE [IoT Agent for UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/) which will receive southbound requests
    using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) and convert them to 
    [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) commands for 
    the devices
  * FIWARE [Cygnus](http://fiware-cygnus.readthedocs.io/en/latest/) which will subscribe to context changes and persist them into a database (**MySQL** , **PostgreSQL**  or **Mongo-DB**)
* One, two or three of the following **Databases**:
  * The underlying [MongoDB](https://www.mongodb.com/) database :
    + Used by the **Orion Context Broker** to hold context data information such as data entities, subscriptions and registrations
    + Used by the **IoT Agent** to hold device information such as device URLs and Keys
    + Potentially used as a data sink to hold historical context data.
  * An additional [PostgreSQL](https://www.postgresql.org/) database :
    + Potentially used as a data sink to hold historical context data.
  * An additional [MySQL](https://www.mysql.com/) database :
     + Potentially used as a data sink to hold historical context data.
* Three **Context Providers**:
  * The **Stock Management Frontend** is not used in this tutorial. It does the following:
    + Display store information and allow users to interact with the dummy IoT devices
    + Show which products can be bought at each store
    + Allow users to "buy" products and reduce the stock count.
  * A webserver acting as set of [dummy IoT devices](https://github.com/Fiware/tutorials.IoT-Sensors) using the [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) protocol running over HTTP.
  * The **Context Provider NGSI** proxy is not used in this tutorial. It does the following:
    + receive requests using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
    + makes requests to publicly available data sources using their own APIs in a proprietory format 
    + returns context data back to the Orion Context Broker in [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) format.

Since all interactions between the elements are initiated by HTTP requests, the entities can be containerized and run from exposed ports. 

The specific architecture of each section of the tutorial is discussed below.


# Start Up

Before you start you should ensure that you have obtained or built the necessary Docker images locally. Please run

```console
./services create
``` 

>**Note** The `context-provider` image has not yet been pushed to Docker hub.
> Failing to build the Docker sources before proceeding will result in the following error:
>
>```
>Pulling context-provider (fiware/cp-web-app:latest)...
>ERROR: The image for the service you're trying to recreate has been removed.
>```


Thereafter, all services can be initialised from the command line by running the [services](https://github.com/Fiware/tutorials.Historic-Context-Flume/blob/master/services) Bash script provided within the repository:

```console
./services <command>
``` 

Where `<command>` will vary depending upon the databases we wish to activate.
This command will also import seed data from the previous tutorials and provision the dummy IoT sensors on startup.

>:information_source: **Note:** If you want to clean up and start over again you can do so with the following command:
>
>```console
>./services stop
>``` 
>
