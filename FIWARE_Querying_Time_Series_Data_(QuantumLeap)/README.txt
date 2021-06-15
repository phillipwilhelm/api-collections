This tutorial is an introduction to
[FIWARE QuantumLeap](https://smartsdk.github.io/ngsi-timeseries-api/) - a
generic enabler which is used to persist context data into a **CrateDB**
database. The tutorial activates the IoT sensors connected in the
[previous tutorial](https://github.com/Fiware/tutorials.IoT-Agent) and persists
measurements from those sensors into the database. To retrieve time-based
aggregations of such data, users can either use **QuantumLeap** query API or
connect directly to the **CrateDB** HTTP endpoint. Results are visualised on a
graph or via the **Grafana** time series analytics tool.

The tutorial uses [cUrl](https://ec.haxx.se/) commands throughout, but is also
available as
[Postman documentation](https://fiware.github.io/tutorials.Time-Series-Data/)

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Time-Series-Data/icon/GitHub-Mark-32px.png) [FIWARE 304: Time-Series Data](https://github.com/Fiware/tutorials.Time-Series-Data)

# Persisting and Querying Time Series Data (CrateDB)

> "Forever is composed of nows."
>
> — Emily Dickinson

[Previous tutorials](https://github.com/Fiware/tutorials.Historic-Context) have
shown how to persist historic context data into a range of databases such as
**MySQL** and **PostgreSQL**. Furthermore, the
[Short Term Historic](https://github.com/Fiware/tutorials.Short-Term-History)
tutorial has introduced the
[STH-Comet](https://fiware-sth-comet.readthedocs.io/) generic enabler for
persisting and querying historic context data using a **MongoDB** database.

FIWARE [QuantumLeap](https://smartsdk.github.io/ngsi-timeseries-api/) is an
alternative generic enabler created specifically for data persistence into the
**CrateDB** time-series database, and therefore offers an alternative to the
[STH-Comet](https://fiware-sth-comet.readthedocs.io/).

[CrateDB](https://crate.io/) is a distributed SQL DBMS designed for use with the
internet of Things. It is capable of ingesting a large number of data points per
second and can be queried in real-time. The database is designed for the
execution of complex queries such as geospatial and time series data. Retrieval
of this historic context data allows for the creation of graphs and dashboards
displaying trends over time.

A summary of the differences can be seen below:

| QuantumLeap                                                                                            | STH-Comet                                                                                          |
| ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| Offers an NGSI v2 interface for notifications                                                          | Offers an NGSI v1 interface for notifications                                                      |
| Persists Data to a CrateDB database                                                                    | Persists Data to MongoDB database                                                                  |
| Offers its own HTTP endpoint for queries, but you can also query CrateDB                               | Offers its own HTTP endpoint for queries - MongoDB database cannot be accessed directly            |
| QuantumLeap supports complex data queries (thanks to CrateDB)                                          | STH-Comet offers a limited set of queries                                                          |
| CrateDB is a distributed and scalable SQL DBMS built atop NoSQL storage                                | MongoDB is a document based NoSQL database                                                         |
| QuantumLeap's API is docummented in OpenAPI [here](https://app.swaggerhub.com/apis/smartsdk/ngsi-tsdb) | STH-Comet's API is explained in its docs [here](https://fiware-sth-comet.readthedocs.io/en/latest) |

Further details about the differences between the underlying database engines
can be found [here](https://db-engines.com/en/system/CrateDB%3BMongoDB).

## Analyzing time series data

The appropriate use of time series data analysis will depend on your use case
and the reliability of the data measurements you receive. Time series data
analysis can be used to answer questions such as:

-   What was the maximum measurement of a device within a given time period?
-   What was the average measurement of a device within a given time period?
-   What was the sum of the measurements sent by a device within a given time
    period?

It can also be used to reduce the significance of each individual data point to
exclude outliers by smoothing.

#### Grafana

[Grafana](https://grafana.com/) is an open source software for time series
analytics tool which will be used during this tutorial. It integrates with a
variety of time-series databases including **CrateDB**. It is available licensed
under the Apache License 2.0. More information can be found at
https://grafana.com/.

#### Device Monitor

For the purpose of this tutorial, a series of dummy IoT devices have been
created, which will be attached to the context broker. Details of the
architecture and protocol used can be found in the
[IoT Sensors tutorial](https://github.com/Fiware/tutorials.IoT-Sensors). The
state of each device can be seen on the UltraLight device monitor web page found
at: `http://localhost:3000/device/monitor`

![FIWARE Monitor](https://fiware.github.io/tutorials.Time-Series-Data/img/device-monitor.png)

#### Device History

Once **QuantumLeap** has started aggregating data, the historical state of each
device can be seen on the device history web page found at:
`http://localhost:3000/device/history/urn:ngsi-ld:Store:001`

![](https://fiware.github.io/tutorials.Time-Series-Data/img/history-graphs.png)

# Architecture

This application builds on the components and dummy IoT devices created in
[previous tutorials](https://github.com/Fiware/tutorials.IoT-Agent/). It will
use three FIWARE components: the
[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/), the
[IoT Agent for Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/),
and [QuantumLeap](https://smartsdk.github.io/ngsi-timeseries-api/) .

Therefore the overall architecture will consist of the following elements:

-   The **FIWARE Generic Enablers**:

    -   The FIWARE
        [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/)
        which will receive requests using
        [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
    -   The FIWARE
        [IoT Agent for Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/)
        which will receive northbound measurements from the dummy IoT devices in
        [Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
        format and convert them to
        [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) requests
        for the context broker to alter the state of the context entities
    -   FIWARE [QuantumLeap](https://smartsdk.github.io/ngsi-timeseries-api/)
        subscribed to context changes and persisting them into a **CrateDB**
        database

-   A [MongoDB](https://www.mongodb.com/) database:

    -   Used by the **Orion Context Broker** to hold context data information
        such as data entities, subscriptions and registrations
    -   Used by the **IoT Agent** to hold device information such as device URLs
        and Keys

-   A [CrateDB](https://crate.io/) database:

    -   Used as a data sink to hold time-based historical context data
    -   offers an HTTP endpoint to interpret time-based data queries

-   A **Context Provider**: - A webserver acting as set of
    [dummy IoT devices](https://github.com/Fiware/tutorials.IoT-Sensors) using
    the
    [Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
    protocol running over HTTP. - Note the **Stock Management Frontend** and
    **Context Provider NGSI** proxy are not used in this tutorial.

Since all interactions between the elements are initiated by HTTP requests, the
entities can be containerized and run from exposed ports.

The overall architecture can be seen below:

![](https://fiware.github.io/tutorials.Time-Series-Data/img/architecture.png)

# Prerequisites

## Docker and Docker Compose

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
applications. A series of
[YAML files](https://raw.githubusercontent.com/Fiware/tutorials.Historic-Context/master/cygnus)
are used to configure the required services for the application. This means all
container services can be brought up in a single command. Docker Compose is
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

## Cygwin for Windows

We will start up our services using a simple Bash script. Windows users should
download [cygwin](http://www.cygwin.com/) to provide a command-line
functionality similar to a Linux distribution on Windows.

# Start Up

Before you start, you should ensure that you have obtained or built the
necessary Docker images locally. Please clone the repository and create the
necessary images by running the commands as shown:

```console
git clone git@github.com:Fiware/tutorials.Time-Series-Data.git
cd tutorials.Time-Series-Data

./services create
```

Thereafter, all services can be initialized from the command-line by running the
[services](https://github.com/Fiware/tutorials.Time-Series-Data/blob/master/services)
Bash script provided within the repository:

```console
./services start
```

> :information_source: **Note:** If you want to clean up and start over again
> you can do so with the following command:
>
> ```console
> ./services stop
> ```

# Connecting FIWARE to a CrateDB Database via QuantumLeap

In the configuration, **QuantumLeap** listens to NGSI v2 notifications on port
`8868` and persists historic context data to the **CrateDB**. **CrateDB** is
accessible using port `4200` and can either be queried directly or attached to
the Grafana analytics tool. The rest of the system providing the context data
has been described in previous tutorials

## CrateDB Database Server Configuration

```yaml
cratedb:
    image: crate:2.3
    hostname: cratedb
    ports:
        - "4200:4200"
        - "4300:4300"
    command:
        -Ccluster.name=democluster -Chttp.cors.enabled=true
        -Chttp.cors.allow-origin="*"
```

## QuantumLeap Configuration

```yaml
quantumleap:
    image: smartsdk/quantumleap
    hostname: quantumleap
    ports:
        - "8668:8668"
    depends_on:
        - cratedb
    environment:
        - CRATE_HOST=cratedb
```

## Grafana Configuration

```yaml
grafana:
    image: grafana/grafana
    depends_on:
        - cratedb
    ports:
        - "3003:3000"
    environment:
        - GF_INSTALL_PLUGINS=crate-datasource,grafana-clock-panel,grafana-worldmap-panel
```

The `quantumleap` container is listening on one port:

-   The Operations for port for QuantumLeap - `8668` is where the service will
    be listening for notifications from the Orion context broker and where users
    can query data from.

The `CRATE_HOST` environment variable defines the location where the data will
be persisted.

The `cratedb` container is listening on two ports:

-   The Admin UI is available on port `4200`
-   The transport protocol is available on `port 4300`

The `grafana` container has connected up port `3000` internally with port `3003`
externally. This is because the Grafana UI is usually available on port `3000`,
but this port has already been taken by the dummy devices UI so it has been
shifted to another port. The Grafana Environment variables are described within
their own [documentation](http://docs.grafana.org/installation/configuration/).
The configuration ensures we will be able to connect to the **CrateDB** database
later on in the tutorial

### Generating Context Data

For the purpose of this tutorial, we must be monitoring a system where the
context is periodically being updated. The dummy IoT Sensors can be used to do
this. Open the device monitor page at `http://localhost:3000/device/monitor` and
unlock a **Smart Door** and switch on a **Smart Lamp**. This can be done by
selecting an appropriate command from the drop down list and pressing the `send`
button. The stream of measurements coming from the devices can then be seen on
the same page:

![](https://fiware.github.io/tutorials.IoT-Sensors/img/door-open.gif)
