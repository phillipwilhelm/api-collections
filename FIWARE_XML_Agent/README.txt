[![FIWARE IoT Agents](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/iot-agents.svg)](https://github.com/FIWARE/catalogue/blob/master/iot-agents/README.md)
[![NGSI v2](https://img.shields.io/badge/NGSI-v2-5dc0cf.svg)](https://fiware-ges.github.io/orion/api/v2/stable/) 

This tutorial a wires up the dummy IoT devices which are responding using a custom [XML](https://www.w3.org/TR/xml11/)
message format. A **custom IoT Agent** is created based on the IoT Agent Node.js
[library](https://iotagent-node-lib.readthedocs.io/en/latest/) and the framework found in the
[IoT Agent for Ultralight](https://fiware-iotagent-ul.readthedocs.io/en/latest/usermanual/index.html#user-programmers-manual)
devices so that measurements can be read and commands can be sent using
[NGSI-v2](https://fiware.github.io/specifications/OpenAPI/ngsiv2) requests sent to the
[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/).

The tutorial uses [cUrl](https://ec.haxx.se/) commands throughout, but is also available as
[Postman documentation](https://fiware.github.io/tutorials.Custom-IoT-Agent/)

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Custom-IoT-Agent/icon/GitHub-Mark-32px.png) [FIWARE 205: Creating a Custom IoT Agent](https://github.com/Fiware/tutorials.Custom-IoT-Agent)

# Passing custom message formats

As defined previously, an IoT Agent is a component that lets a group of devices send their data to and be managed from a
Context Broker using their own native protocols. Every IoT Agent is defined for a single payload format, although they
may be able to use multiple disparate transports for that payload.

IoT Agents for many standard payloads exist, however it is possible to envisage that additional payloads may be needed
as many potential sources of context data have already their own well-defined de-facto or de-jure standards for passing
data around systems. As an example the **ISOXML** standard
[iso:11783](https://www.iso.org/obp/ui/#iso:std:iso:11783:-10:ed-2:v1:en) is frequently used with Agricultural
Machinery.

The process for creating your own IoT Agent is relatively simple. It is best achieved through selecting an IoT Agent
which uses the required data transport and rewriting/amending the payload processing code to handle the payloads in
question.

For the purpose of this tutorial we will amend code from the existing Ultralight IoT Agent to process a similar custom
XML format. A direct comparison of the two IoT Agents can be seen below:

| IoT Agent for Ultralight                                            | IoT Agent for JSON                                                                    | Protocol's Area of Concern |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | -------------------------- |
| Sample Measure `c\|1`                                               | Sample Measure `<measure device="lamp002" key="xxx">`<br/>&nbsp;`<c value="1"/>`<br/> |
| `</measure>`                                                        | Message Payload                                                                       |
| Sample Command `Robot1@turn\|left=30`                               | Sample Command `<turn device="Robot1">`<br/>&nbsp;`<left>30</left>`<br/>`</turn>`     | Message Payload            |
| Content Type is `text/plain`                                        | Content Type is `application/xml`                                                     | Message Payload            |
| Offers 3 transports - HTTP, MQTT and AMPQ                           | Offers 3 transports - HTTP, MQTT and AMPQ                                             | Transport Mechanism        |
| HTTP listens for measures on `iot/d` by default                     | HTTP listens for measures on `iot/xml` by default                                     | Transport Mechanism        |
| HTTP devices are identified by parameters `?i=XXX&k=YYY`            | HTTP devices are identified by payload `<measure device="XXX" key="YYY">`             | Device Identification      |
| HTTP commands posted to a well-known URL - response is in the reply | HTTP commands posted to a well-known URL - response is in the reply                   | Communications Handshake   |
| MQTT devices are identified by the path of the topic `/XXX/YYY`     | MQTT devices are identified by the path of the topic `/XXX/YYY`                       | Device Identification      |
| MQTT commands posted to the `cmd` topic                             | MQTT commands posted to the `cmd` topic                                               | Communications Handshake   |
| MQTT command responses posted to the `cmdexe` topic                 | MQTT commands posted to the `cmdexe` topic                                            | Communications Handshake   |

As can be seen, the supported communications transports (HTTP, MQTT, AMPQ) remain the same, it is processing of the
custom payload which will need to be adapted to ensure that the XML devices can communicate with the IoT Agent.

It should be noted that, depending on your use case, it also may be necessary to create an additional middleware for
communications purposes. In this example the _devices_ are capable of sending measures and listening and responding to
commands directly on two separate comms channels. A different paradigm is used within the
[LoRaWAN](https://fiware-lorawan.readthedocs.io) and [OPC-UA](https://iotagent-opcua.readthedocs.io) IoT Agents where an
HTTP middleware responds to the IoT Agent, and it is then responsible for converting the communications to the
lower-level CoAP transport used by the devices.

## The teaching goal of this tutorial

The aim of this tutorial is to improve developer understanding of how to create their own custom IoT Agents, a series of
simple modificiations has been made to the code of the Ultralight IoT Agent demonstrating how to make changes. The
tutorial consists of a walk-through of the relevant code and a series of HTTP requests to connect the new IoT Agent. The
code can be found within the current
[GitHub Repository](https://github.com/FIWARE/tutorials.Custom-IoT-Agent/tree/master/iot-agent)

## Reusing Common Functionality

The benefit of modifying an existing IoT Agent is that the developer will be able to reuse the common functionality
found across all IoT Agents. This includes functions such as:

-   Offering a standard location to listen to device updates
-   Offering a standard location to listen to context data updates
-   Holding a list of devices and mapping context data attributes to device syntax
-   Security Authorization

This base functionality has been abstracted out into a common
[IoT Agent framework library](https://iotagent-node-lib.readthedocs.io/)

#### Device Monitor

For the purpose of this tutorial, a series of dummy IoT devices have been created, which will be attached to the context
broker. Details of the architecture and protocol used can be found in the
[IoT Sensors tutorial](https://github.com/FIWARE/tutorials.IoT-Sensors) The state of each device can be seen on the JSON
device monitor web page found at: `http://localhost:3000/device/monitor`

![FIWARE Monitor](https://fiware.github.io/tutorials.IoT-Agent-JSON/img/device-monitor.png)

# Architecture

This application builds on the components created in
[previous tutorials](https://github.com/FIWARE/tutorials.Subscriptions/). It will make use of one FIWARE component - the
[Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) plus a **Custom IoT Agent for XML**. Usage of the
Orion Context Broker is sufficient for an application to qualify as _“Powered by FIWARE”_. Both the Orion Context Broker
and the IoT Agent and rely on open source [MongoDB](https://www.mongodb.com/) technology to keep persistence of the
information they hold. We will also be using the dummy IoT devices created in the
[previous tutorial](https://github.com/FIWARE/tutorials.IoT-Sensors/), however they have been already been adapted to
respond to the custom XML messaging format.

Therefore the overall architecture will consist of the following elements:

-   The FIWARE [Orion Context Broker](https://fiware-orion.readthedocs.io/en/latest/) which will receive requests using
    [NGSI-v2](https://fiware.github.io/specifications/OpenAPI/ngsiv2)
-   The **Custom IoT Agent for XML** which will receive southbound requests using
    [NGSI-v2](https://fiware.github.io/specifications/OpenAPI/ngsiv2) and convert them to XML commands for the devices
-   The underlying [MongoDB](https://www.mongodb.com/) database :
    -   Used by the **Orion Context Broker** to hold context data information such as data entities, subscriptions and
        registrations
    -   Used by the **IoT Agent** to hold device information such as device URLs and Keys
-   A webserver acting as set of [dummy IoT devices](https://github.com/FIWARE/tutorials.IoT-Sensors) using the custom
    XML messaging protocol running over HTTP.

Since all interactions between the elements are initiated by HTTP requests, the entities can be containerized and run
from exposed ports.

![](https://fiware.github.io/tutorials.IoT-Agent-JSON/img/architecture.png)

The necessary configuration information for wiring up the IoT devices and the IoT Agent can be seen in the services
section of the associated `docker-compose.yml` file:

## Dummy IoT Devices Configuration

```yaml
tutorial:
    image: fiware/tutorials.context-provider
    hostname: iot-sensors
    container_name: fiware-tutorial
    networks:
        - default
    expose:
        - "3000"
        - "3001"
    ports:
        - "3000:3000"
        - "3001:3001"
    environment:
        - "DEBUG=tutorial:*"
        - "PORT=3000"
        - "IOTA_HTTP_HOST=iot-agent"
        - "IOTA_HTTP_PORT=7896"
        - "DUMMY_DEVICES_PORT=3001"
        - "DUMMY_DEVICES_API_KEY=4jggokgpepnvsb2uv4s40d59ov"
        - "DUMMY_DEVICES_TRANSPORT=HTTP"
        - "DUMMY_DEVICES_PAYLOAD=XML"
```

The `tutorial` container is listening on two ports:

-   Port `3000` is exposed so we can see the web page displaying the Dummy IoT devices.
-   Port `3001` is exposed purely for tutorial access - so that cUrl or Postman can make JSON commands without being
    part of the same network.

The `tutorial` container is driven by environment variables as shown:

| Key                     | Value                        | Description                                                                                                                        |
| ----------------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| DEBUG                   | `tutorial:*`                 | Debug flag used for logging                                                                                                        |
| WEB_APP_PORT            | `3000`                       | Port used by web-app which displays the dummy device data                                                                          |
| IOTA_HTTP_HOST          | `iot-agent`                  | The hostname of the IoT Agent for JSON - see below                                                                                 |
| IOTA_HTTP_PORT          | `7896`                       | The port that the IoT Agent for JSON will be listening on. `7896` is a common default for JSON over HTTP                           |
| DUMMY_DEVICES_PORT      | `3001`                       | Port used by the dummy IoT devices to receive commands                                                                             |
| DUMMY_DEVICES_API_KEY   | `4jggokgpepnvsb2uv4s40d59ov` | Random security key used for IoT interactions - used to ensure the integrity of interactions between the devices and the IoT Agent |
| DUMMY_DEVICES_TRANSPORT | `HTTP`                       | The transport protocol used by the dummy IoT devices                                                                               |
| DUMMY_DEVICES_PAYLOAD   | `XML`                        | The message payload protocol by the dummy IoT devices                                                                              |

The other `tutorial` container configuration values described in the YAML file are not used in this tutorial.

## Custom XML IoT Agent configuration

The code for the custom XML IoT Agent can be found within the
[GitHub Repository](https://github.com/FIWARE/tutorials.Custom-IoT-Agent/tree/master/iot-agent) associated to this
tutorial. It is a copy of the 1.12.0 version of the IoT Agent for Ultralight, lightly modified as described below. The
associated [Dockerfile](https://github.com/FIWARE/tutorials.Custom-IoT-Agent/blob/master/iot-agent/Dockerfile) merely
copies the code into an appropiate location within a Docker container running Node.js. This allows the component to be
instansiated using a `docker-compose.yaml` file. The necessary configuration can be seen below:

```yaml
iot-agent:
    image: fiware/iotagent-xml
    build:
        context: iot-agent
        dockerfile: Dockerfile
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
        - IOTA_CB_HOST=orion
        - IOTA_CB_PORT=1026
        - IOTA_NORTH_PORT=4041
        - IOTA_REGISTRY_TYPE=mongodb
        - IOTA_LOG_LEVEL=DEBUG
        - IOTA_TIMESTAMP=true
        - IOTA_CB_NGSI_VERSION=v2
        - IOTA_AUTOCAST=true
        - IOTA_MONGO_HOST=mongo-db
        - IOTA_MONGO_PORT=27017
        - IOTA_MONGO_DB=iotagentjson
        - IOTA_HTTP_PORT=7896
        - IOTA_PROVIDER_URL=http://iot-agent:4041
        - IOTA_DEFAULT_RESOURCE=/iot/xml
```

The `iot-agent` container relies on the precence of the Orion Context Broker and uses a MongoDB database to hold device
information such as device URLs and Keys. The container is listening on two ports:

-   Port `7896` is exposed to receive JSON measurements over HTTP from the Dummy IoT devices
-   Port `4041` is exposed purely for tutorial access - so that cUrl or Postman can make provisioning commands without
    being part of the same network.

The `iot-agent` container is driven by environment variables as shown:

| Key                   | Value                   | Description                                                                                                                                           |
| --------------------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| IOTA_CB_HOST          | `orion`                 | Hostname of the context broker to update context                                                                                                      |
| IOTA_CB_PORT          | `1026`                  | Port that context broker listens on to update context                                                                                                 |
| IOTA_NORTH_PORT       | `4041`                  | Port used for Configuring the IoT Agent and receiving context updates from the context broker                                                         |
| IOTA_REGISTRY_TYPE    | `mongodb`               | Whether to hold IoT device info in memory or in a database                                                                                            |
| IOTA_LOG_LEVEL        | `DEBUG`                 | The log level of the IoT Agent                                                                                                                        |
| IOTA_TIMESTAMP        | `true`                  | Whether to supply timestamp information with each measurement received from attached devices                                                          |
| IOTA_CB_NGSI_VERSION  | `v2`                    | Whether to supply use NGSI v2 when sending updates for active attributes                                                                              |
| IOTA_AUTOCAST         | `true`                  | Ensure JSON number values are read as numbers not strings                                                                                             |
| IOTA_MONGO_HOST       | `context-db`            | The hostname of mongoDB - used for holding device information                                                                                         |
| IOTA_MONGO_PORT       | `27017`                 | The port mongoDB is listening on                                                                                                                      |
| IOTA_MONGO_DB         | `iotagentjson`          | The name of the database used in mongoDB                                                                                                              |
| IOTA_HTTP_PORT        | `7896`                  | The port where the IoT Agent listens for IoT device traffic over HTTP                                                                                 |
| IOTA_PROVIDER_URL     | `http://iot-agent:4041` | URL passed to the Context Broker when commands are registered, used as a forwarding URL location when the Context Broker issues a command to a device |
| IOTA_DEFAULT_RESOURCE | `/iot/xml`              | The default path the IoT Agent uses listenening for custom XML measures.                                                                              |