[![FIWARE Core Context Management](https://nexus.lab.fiware.org/static/badges/chapters/core.svg)](https://github.com/FIWARE/catalogue/blob/master/processing/README.md)

This tutorial is an introduction to the [FIWARE Cosmos Orion Flink Connector](http://fiware-cosmos-flink.rtfd.io), which
facilitates Big Data analysis of context data, through an integration with [Apache Flink](https://flink.apache.org/),
one of the most popular Big Data platforms. Apache Flink is a framework and distributed processing engine for stateful
computations both over unbounded and bounded data streams. Flink has been designed to run in all common cluster
environments, perform computations at in-memory speed and at any scale.

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Big-Data-Flink/icon/GitHub-Mark-32px.png) [https://github.com/FIWARE/tutorials.Big-Data-Flink](https://github.com/FIWARE/tutorials.Big-Data-Flink)


# Real-time Processing and Big Data Analysis

> "Who controls the past controls the future: who controls the present controls the past."
>
> — George Orwell. "1984" (1949)

Smart solutions based on FIWARE are architecturally designed around microservices. They are therefore are designed to
scale-up from simple applications (such as the Supermarket tutorial) through to city-wide installations base on a large
array of IoT sensors and other context data providers.

The massive amount of data involved enventually becomes too much for a single machine to analyse, process and store, and
therefore the work must be delegated to additional distributed services. These distributed systems form the basis of
so-called **Big Data Analysis**. The distribution of tasks allows developers to be able to extract insights
from huge data sets which would be too complex to be dealt with using traditional methods. and uncover hidden patterns
and correlations.

As we have seen, context data is core to any Smart Solution, and the Context Broker is able to monitor changes of state
and raise [subscription events](https://github.com/Fiware/tutorials.Subscriptions) as the context changes. For smaller
installations, each subscription event can be processed one-by-one by a single receiving endpoint, however as the system
grows, another technique will be required to avoid overwhelming the listener, potentially blocking resources and missing
updates.

**Apache Flink** is a Java/Scala based stream-processing framework which enables the delegation of data-flow processes.
Therefore additional computational resources can be called upon to deal with data as events arrive. The **Cosmos Flink**
connector allows developers write custom business logic to listen for context data subscription events and then process
the flow of the context data. Flink is able to delegate these actions to other workers where they will be acted upon
either in sequentiallly or in parallel as required. The data flow processing itself can be arbitrarily complex.

Obviously in reality our existing Supermarket scenario is far too small to require the use of a Big Data solution, but
will serve as a basis for demonstrating the type of real-time processing which may be required in a larger solution
which is processing a continous stream of context-data events.

# Architecture

This application builds on the components and dummy IoT devices created in
[previous tutorials](https://github.com/FIWARE/tutorials.IoT-Agent/). It will make use of three FIWARE components - the
[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/), the
[IoT Agent for Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/), and the
[Cosmos Orion Flink Connector](https://fiware-cosmos-flink.readthedocs.io/en/latest/) for connecting Orion to an
[Apache Flink cluster](https://ci.apache.org/projects/flink/flink-docs-stable/concepts/runtime.html). The Flink cluster
itself will consist of a single **JobManager** _master_ to coordinate execution and a single **TaskManager** _worker_ to
execute the tasks.

Both the Orion Context Broker and the IoT Agent rely on open source [MongoDB](https://www.mongodb.com/) technology to
keep persistence of the information they hold. We will also be using the dummy IoT devices created in the
[previous tutorial](https://github.com/FIWARE/tutorials.IoT-Agent/).

Therefore the overall architecture will consist of the following elements:

-   Two **FIWARE Generic Enablers** as independent microservices:
    -   The FIWARE [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) which will receive requests
        using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
    -   The FIWARE [IoT Agent for Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/) which will
        receive northbound measurements from the dummy IoT devices in
        [Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
        format and convert them to [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) requests for the
        context broker to alter the state of the context entities
- An [Apache Flink cluster](https://ci.apache.org/projects/flink/flink-docs-stable/concepts/runtime.html) consisting of a single **JobManager** and a single **TaskManager**
    -   The FIWARE [Cosmos Orion Flink Connector](https://fiware-cosmos-flink.readthedocs.io/en/latest/) will be deployed as part of the dataflow which will
        subscribe to context changes and make operations on them in real-time
-   One [MongoDB](https://www.mongodb.com/) **database** :
    -   Used by the **Orion Context Broker** to hold context data information such as data entities, subscriptions
        and registrations
    -   Used by the **IoT Agent** to hold device information such as device URLs and Keys
-   Three **Context Providers**:
    -   A webserver acting as set of [dummy IoT devices](https://github.com/FIWARE/tutorials.IoT-Sensors) using the
        [Ultralight 2.0](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
        protocol running over HTTP.
    -   The **Stock Management Frontend** is not used in this tutorial. It does the following:
        -   Display store information and allow users to interact with the dummy IoT devices
        -   Show which products can be bought at each store
        -   Allow users to "buy" products and reduce the stock count.
    -   The **Context Provider NGSI** proxy is not used in this tutorial. It does the following:
        -   receive requests using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
        -   makes requests to publicly available data sources using their own APIs in a proprietary format
        -   returns context data back to the Orion Context Broker in
            [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) format.

The overall architecture can be seen below:

![](https://fiware.github.io/tutorials.Big-Data-Flink/img/architecture.png)

Since all interactions between the elements are initiated by HTTP requests, the entities can be containerized and run
from exposed ports.

The configuration information of the Apache Flink cluster can be seen in the `jobmanager` and `taskmanager` sections of
the associated `docker-compose.yml` file:

## Flink Cluster Configuration

```yaml
jobmanager:
    image: flink:1.9.0-scala_2.11
    hostname: jobmanager
    container_name: flink-jobmanager
    expose:
        - "8081"
        - "9001"
    ports:
        - "6123:6123"
        - "8081:8081"
        - "9001:9001"
    command: jobmanager
    environment:
        - JOB_MANAGER_RPC_ADDRESS=jobmanager
```

```yaml
taskmanager:
    image: flink:1.9.0-scala_2.11
    hostname: taskmanager
    container_name: flink-taskmanager
    ports:
        - "6121:6121"
        - "6122:6122"
    depends_on:
        - jobmanager
    command: taskmanager
    links:
        - "jobmanager:jobmanager"
    environment:
        - JOB_MANAGER_RPC_ADDRESS=jobmanager
```

The `jobmanager` container is listening on three ports:

-   Port `8081` is exposed so we can see the web front-end of the Apache Flink Dashobard
-   Port `9001` is exposed so that the installation can recieve context data subscriptions
-   Port `6123` is the standard **JobManager** RPC port, used for internal communications

The `taskmanager` container is listening on two ports:

-   Ports `6121` and `6122` are used and RPC ports by the **TaskManager**, used for internal communications

The containers within the flink cluster are driven by a single environment variable as shown:

| Key                     | Value        | Description                                                           |
| ----------------------- | ------------ | --------------------------------------------------------------------- |
| JOB_MANAGER_RPC_ADDRESS | `jobmanager` | URL of the _master_ Job Manager which coordinates the task processing |

# Prerequisites

## Docker and Docker Compose

To keep things simple, all components will be run using [Docker](https://www.docker.com). **Docker** is a container
technology which allows to different components isolated into their respective environments.

-   To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
-   To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
-   To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A series of
[YAML files](https://github.com/FIWARE/tutorials.Big-Data-Flink/tree/master/docker-compose) are used to configure the
required services for the application. This means all container services can be brought up in a single command. Docker
Compose is installed by default as part of Docker for Windows and Docker for Mac, however Linux users will need to
follow the instructions found [here](https://docs.docker.com/compose/install/)

You can check your current **Docker** and **Docker Compose** versions using the following commands:

```console
docker-compose -v
docker version
```

Please ensure that you are using Docker version 18.03 or higher and Docker Compose 1.21 or higher and upgrade if
necessary.

## Maven

[Apache Maven](https://maven.apache.org/download.cgi) is a software project management and comprehension tool. Based on
the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a
central piece of information. We will use Maven to define and download our dependencies and to build and package our
code into a JAR file.

## Cygwin for Windows

We will start up our services using a simple Bash script. Windows users should download [cygwin](http://www.cygwin.com/)
to provide a command-line functionality similar to a Linux distribution on Windows.

# Start Up

Before you start, you should ensure that you have obtained or built the necessary Docker images locally. Please clone
the repository and create the necessary images by running the commands shown below. Note that you might need to run some
of the commands as a privileged user:

```console
git clone https://github.com/FIWARE/tutorials.Big-Data-Flink.git
cd tutorials.Big-Data-Flink
./services create
```

This command will also import seed data from the previous tutorials and provision the dummy IoT sensors on startup.

To start the system, run the following command:

```console
./services start
```

>  **Note:** If you want to clean up and start over again you can do so with the following command:
>
> ```
> ./services stop
> ```

# Real-time Processing Operations

Dataflow within **Apache Flink** is defined within the
[Flink documentation](https://ci.apache.org/projects/flink/flink-docs-release-1.9/concepts/programming-model.html) as
follows:

> "The basic building blocks of Flink programs are streams and transformations. Conceptually a stream is a (potentially
> never-ending) flow of data records, and a transformation is an operation that takes one or more streams as input, and
> produces one or more output streams as a result.
>
> When executed, Flink programs are mapped to streaming dataflows, consisting of streams and transformation operators.
> Each dataflow starts with one or more sources and ends in one or more sinks. The dataflows resemble arbitrary directed
> acyclic graphs (DAGs). Although special forms of cycles are permitted via iteration constructs, for the most part this
> can be glossed over this for simplicity."

![](https://fiware.github.io/tutorials.Big-Data-Flink/img/streaming-dataflow.png)

This means that to create a streaming data flow we must supply the following:

-   A mechanism for reading Context data as a **Source Operator**
-   Business logic to define the transform operations
-   A mechanism for pushing Context data back to the context broker as a **Sink Operator**

The `orion-flink.connect.jar` offers both **Source** and **Sink** operations. It therefore only remains to write the
necessary Scala code to connect the streaming dataflow pipeline operations together. The processing code can be complied
into a JAR file which can be uploaded to the flink cluster. Two examples will be detailed below, all the source code for
this tutorial can be found within the
[cosmos-examples](https://github.com/FIWARE/tutorials.Big-Data-Flink/tree/master/cosmos-examples) directory.

Further Flink processing examples can be found on the
[Apache Flink website](https://ci.apache.org/projects/flink/flink-docs-release-1.9/getting-started)

### Compiling a JAR file for Flink

An existing `pom.xml` file has been created which holds the necessary prerequisites to build the examples JAR file

In order to use the Orion Flink Connector we first need to manually install the connector JAR as an artifact using
Maven:

```console
cd cosmos-examples
mvn install:install-file \
  -Dfile=./orion.flink.connector-1.2.1.jar \
  -DgroupId=org.fiware.cosmos \
  -DartifactId=orion.flink.connector \
  -Dversion=1.2.1 \
  -Dpackaging=jar
```

Thereafter the source code can be compiled by running the `mvn package` command within the same directory:

```console
cd cosmos-examples
mvn package
```

A new JAR file called `cosmos-examples-1.0.jar` will be created within the `cosmos-examples/target` directory.

### Generating a stream of Context Data

For the purpose of this tutorial, we must be monitoring a system in which the context is periodically being updated. The
dummy IoT Sensors can be used to do this. Open the device monitor page at `http://localhost:3000/device/monitor` and
unlock a **Smart Door** and switch on a **Smart Lamp**. This can be done by selecting an appropriate the command from
the drop down list and pressing the `send` button. The stream of measurements coming from the devices can then be seen
on the same page:

![](https://fiware.github.io/tutorials.Big-Data-Flink/img/door-open.gif)