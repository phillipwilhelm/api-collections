This tutorial uses introduces the use of the MQTT protocol across IoT devices connecting to FIWARE. The [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) IoT Agent
created in the [previous tutorial](https://github.com/Fiware/tutorials.IoT-Agent) is reconfigured to
communicate with a set of dummy IoT devices using MQTT

# What is MQTT?

MQTT is publish-subscribe-based messaging protocol used in the Internet of Things. It works on top of the TCP/IP
protocol, and is designed for connections with remote locations where a "small code footprint" is required or the
network bandwidth is limited. The goal is to provide a protocol, which is bandwidth-efficient and uses little
battery power.

The [previous tutorial](https://github.com/Fiware/tutorials.IoT-Agent) used HTTP as its transport mechanism between
the devices and the IoT Agent. HTTP uses a request/response paradigm where each device connects directly to the IoT Agent.
MQTT is different in that publish-subscribe is event-driven and pushes messages to clients. It requires an additional
central communication point (known as the MQTT broker) which it is in charge of dispatching all messages between the senders and the rightful receivers. Each client that publishes a message to the broker, includes a **topic** into the message. The **topic** is the routing information for the broker. Each client that wants to receive messages subscribes to a certain **topic** and the broker delivers all messages with the matching **topic** to the client. Therefore the clients don’t have to know each other, they only communicate over the **topic**. This architecture enables highly scalable solutions without dependencies between the data producers and the data consumers.


The UltraLight 2.0 IoT Agent will only send or interpret messages using the [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) syntax,
however it can be used to send and receive messages over multiple **transport** mechanisms. Therefore we
are able to use the same FIWARE generic enabler to connect to a wider range of IoT devices.

#### Mosquitto MQTT Broker

[Mosquitto](https://mosquitto.org/) is a readily available, open source MQTT broker which will be used during this tutorial.
It is available licensed under EPL/EDL. More information can be found at https://mosquitto.org/


#### Device Monitor

For the purpose of this tutorial, a series of dummy IoT devices have been created, which will be attached to the context broker. Details of the architecture and protocol used can be found in the [IoT Sensors tutorial](https://github.com/Fiware/tutorials.IoT-Sensors)
The state of each device can be seen on the UltraLight device monitor web-page found at: `http://localhost:3000/device/monitor`

![FIWARE Monitor](https://fiware.github.io/tutorials.IoT-over-MQTT/img/device-monitor.png)

# Architecture

This application builds on the components created in [previous tutorials](https://github.com/Fiware/tutorials.IoT-Agent/). It
will make use of two FIWARE components - the [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) and the [IoT Agent for UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/). Usage of the Orion Context Broker is sufficient for an application to qualify as *“Powered by FIWARE”*.
Both the Orion Context Broker and the IoT Agent rely on open source [MongoDB](https://www.mongodb.com/) technology to keep persistence of the information they hold. We will also be using the dummy IoT devices created in the [previous tutorial](https://github.com/Fiware/tutorials.IoT-Agent/) 
Additionally will add an instance of the [Mosquitto](https://mosquitto.org/) MQTT broker which is open source and available under the EPL/EDL.


Therefore the overall architecture will consist of the following elements:

* The FIWARE [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) which will receive requests using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
* The FIWARE [IoT Agent for UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/) which will:
 + receive southbound requests using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) and convert them to  [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) MQTT topics for the MQTT Broker
 + listen to the **MQTT Broker** on registered topics to send measurements northbound
* The [Mosquitto](https://mosquitto.org/) **MQTT Broker** which acts as a central communication point, passing 
  MQTT topics between the **IoT Agent** and IoT devices as necessary.
* The underlying [MongoDB](https://www.mongodb.com/) database :
  + Used by the **Orion Context Broker** to hold context data information such as data entities, subscriptions and registrations
  + Used by the **IoT Agent** to hold device information such as device URLs and Keys
* A webserver acting as set of [dummy IoT devices](https://github.com/Fiware/tutorials.IoT-Sensors) using the [UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual) protocol running over MQTT.
* The **Context Provider NGSI** proxy is not used in this tutorial. It does the following:
  + receive requests using [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
  + makes requests to publicly available data sources using their own APIs in a proprietary format 
  + returns context data back to the Orion Context Broker in [NGSI](https://fiware.github.io/specifications/OpenAPI/ngsiv2) format.
* The **Stock Management Frontend**  is not used in this tutorial will it does the following:
  + Display store information
  + Show which products can be bought at each store
  + Allow users to "buy" products and reduce the stock count.


Since all interactions between the elements are initiated by HTTP or MQTT requests over TCP, the entities can be containerized and run from exposed ports. 

![](https://fiware.github.io/tutorials.IoT-over-MQTT/img/architecture.png)

The necessary configuration information for wiring up the Mosquitto MQTT Broker, the IoT devices and the IoT Agent can be seen in the services section of the associated `docker-compose.yml`  file:

## Mosquitto Configuration

```yaml
  mosquitto:
    image: eclipse-mosquitto
    hostname: mosquitto
    container_name: mosquitto
    networks:
        - default
    expose:
        - "1883"
        - "9001"
    ports:
        - "1883:1883"
        - "9001:9001"
    volumes:
      - ./mosquitto/mosquitto.conf:/mosquitto/config/mosquitto.conf
    
```

The `mosquitto` container is listening on two ports: 

* Port `3000` is exposed so we can post MQTT topics
* Port `9001` is the standard port for HTTP/Websocket communications

The attached volume is a [configuration file](https://github.com/Fiware/tutorials.IoT-over-MQTT/blob/master/osquitto/mosquitto.conf) used to increase the debug level of the MQTT Message Broker.

## Dummy IoT Devices Configuration

```yaml
  context-provider:
    image: fiware/cp-web-app:latest
    hostname: context-provider
    container_name: context-provider
    networks:
        - default
    expose:
        - "3000"
        - "3001"
    ports:
        - "3000:3000"
        - "3001:3001"
    environment:
        - "DEBUG=proxy:*"
        - "PORT=3000"
        - "DUMMY_DEVICES_PORT=3001"
        - "DUMMY_DEVICES_API_KEY=4jggokgpepnvsb2uv4s40d59ov"
        - "DUMMY_DEVICES_TRANSPORT=MQTT"
```

The `context-provider` container is listening on two ports: 

* Port `3000` is exposed so we can see the web-page displaying the Dummy IoT devices.
* Port `3001` is exposed purely for tutorial access - so that cUrl or Postman can make UltraLight commands
  without being part of the same network.


The `context-provider` container is driven by environment variables as shown:

| Key |Value|Description|
|-----|-----|-----------|
|DEBUG|`proxy:*`| Debug flag used for logging |
|PORT|`3000`|Port used by web-app which displays the dummy device data |
|DUMMY_DEVICES_PORT|`3001`|Port used by the dummy IoT devices to receive commands |
|DUMMY_DEVICES_API_KEY|`4jggokgpepnvsb2uv4s40d59ov`| Random security key used for UltraLight interactions - used to ensure the integrity of interactions between the devices and the IoT Agent |

The other `context-provider` container configuration values described in the YAML file are not used in this tutorial.

## IoT Agent for UltraLight 2.0 Configuration

The [IoT Agent for UltraLight 2.0](http://fiware-iotagent-ul.readthedocs.io/en/latest/)  can be instantiated within a Docker container. An official Docker image is available from [Docker Hub](https://hub.docker.com/r/fiware/iotagent-ul/) tagged `fiware/iotagent-ul`. The 
necessary configuration can be seen below:

```yaml
  iot-agent:
    image: fiware/iotagent-ul:latest
    hostname: iot-agent
    container_name: fiware-iot-agent
    depends_on:
      - mongo-db
    networks:
        - default
    expose:
        - "4041"
        - "7896"
    ports:
        - "4041:4041"
        - "7896:7896"
    environment:
        - "IOTA_CB_HOST=orion"
        - "IOTA_CB_PORT=1026"
        - "IOTA_NORTH_PORT=4041"
        - "IOTA_REGISTRY_TYPE=mongodb"
        - "IOTA_LOG_LEVEL=DEBUG"
        - "IOTA_TIMESTAMP=true"
        - "IOTA_MONGO_HOST=mongo-db"
        - "IOTA_MONGO_PORT=27017"
        - "IOTA_MONGO_DB=iotagentul"
        - "IOTA_PROVIDER_URL=http://iot-agent:4041"
        - "IOTA_MQTT_HOST=mosquitto"
        - "IOTA_MQTT_PORT=1883"
```

The `iot-agent` container relies on the precence of the Orion Context Broker and uses a MongoDB database to hold device information such as device URLs and Keys. The container is listening on two ports: 

* Port `7896` is exposed to receive Ultralight measurements over HTTP from the Dummy IoT devices
* Port `4041` is exposed purely for tutorial access - so that cUrl or Postman can make provisioning commands
  without being part of the same network.


The `iot-agent` container is driven by environment variables as shown:

| Key |Value|Description|
|-----|-----|-----------|
|IOTA_CB_HOST|`orion`| Hostname of the context broker to update context |
|IOTA_CB_PORT|`1026`| Port that context broker listens on to update context |
|IOTA_NORTH_PORT|`4041` | Port used for Configuring the IoT Agent and receiving context updates from the context broker |
|IOTA_REGISTRY_TYPE|`mongodb`| Whether to hold IoT device info in memory or in a database |
|IOTA_LOG_LEVEL|`DEBUG`|The log level of the IoT Agent |
|IOTA_TIMESTAMP|`true`| Whether to supply timestamp information with each measurement received from attached devices |
|IOTA_MONGO_HOST|`context-db`| The host name of mongoDB - used for holding device information |
|IOTA_MONGO_PORT|`27017`| The port mongoDB is listening on |
|IOTA_MONGO_DB|`iotagentul`| The name of the database used in mongoDB |
|IOTA_PROVIDER_URL|`http://iot-agent:4041`| URL passed to the Context Broker when commands are registered, used as a forwarding URL location when the Context Broker issues a command to a device | 
|IOTA_MQTT_HOST|`mosquitto`| The host name of the MQTT Broker  |
|IOTA_MQTT_PORT|`1883`| The port the MQTT Broker is listening on to receive topics |

As you can see, use of the MQTT transport is driven by only two environment variables `IOTA_MQTT_HOST` and `IOTA_MQTT_PORT`

# Prerequisites

## Docker and Docker Compose 

To keep things simple all components will be run using [Docker](https://www.docker.com). **Docker** is a container technology which allows to different components isolated into their respective environments. 

* To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
* To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
* To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A 
[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.IoT-over-MQTT/master/docker-compose.yml) is used
configure the required services for the application. This means all container services can be brought up in a single 
command. Docker Compose is installed by default  as part of Docker for Windows and  Docker for Mac, however Linux users 
will need to follow the instructions found  [here](https://docs.docker.com/compose/install/)
## Cygwin for Windows

We will start up our services using a simple Bash script. Windows users should download [cygwin](http://www.cygwin.com/) to provide a command line functionality similar to a Linux distribution on Windows.


# Start Up

Before you start you should ensure that you have obtained or built the necessary Docker images locally. Please clone the repository and create the necessary images by running the commands as shown:

```console
git clone git@github.com:Fiware/tutorials.IoT-over-MQTT.git
cd tutorials.IoT-over-MQTT

./services create
``` 

>**Note** The `context-provider` image has not yet been pushed to Docker hub.
> Failing to build the Docker sources before proceeding will result in the following error:
>
>```
>Pulling context-provider (fiware/cp-web-app:latest)...
>ERROR: The image for the service you're trying to recreate has been removed.
>```


Thereafter, all services can be initialized from the command line by running the [services](https://github.com/Fiware/tutorials.IoT-over-MQTT/blob/master/services) Bash script provided within the repository:

```console
./services start
``` 

>:information_source: **Note:** If you want to clean up and start over again you can do so with the following command:
>
>```console
>./services stop
>``` 
>



