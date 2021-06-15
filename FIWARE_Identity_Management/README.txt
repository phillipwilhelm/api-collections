This tutorial is an introduction to [FIWARE Keyrock](http://fiware-idm.readthedocs.io/en/latest/) - a generic enabler which introduces
**Identity Management** into FIWARE services. The tutorial explains how to create users and organizations in preparation to assign
roles and permissions to them in a later tutorial.

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Identity-Management/icon/GitHub-Mark-32px.png) [FIWARE 401: Identity Management](https://github.com/Fiware/tutorials.Identity-Management)

# Identity Management

> "If one meets a powerful person — ask them five questions: ‘What power have you got?
> Where did you get it from? In whose interests do you exercise it? To whom are you
> accountable? And how can we get rid of you?’"
>
> — Anthony Wedgwood Benn (The Five Essential Questions of Democracy)


In computer security terminology, Identity management is the security and business discipline that "enables the right
individuals to access the right resources at the right times and for the right reasons". It addresses the need to
ensure appropriate access to resources across disparate systems.

The FIWARE framework consists of a series of separate components, and the security chapter aims to implement
the common needs of these components regarding who (or what) gets to access which resources within the system,
but before access to resources can be locked down, the identity of the person (or service) making the request
needs to be known. The FIWARE **Keyrock** Generic Enabler sets up all of the common characteristics of an
Identity Management System out-of-the-box, so that other components are able to use standard authentication
mechanisms to  accept or reject requests based on industry standard protocols.

Identity Management therefore covers the issues of how to gain an identity within the system, the protection
of that identity and the surrounding technologies such as passwords and network protocols.

## Standard Concepts of Identity Management

The following common objects are found with the **Keyrock** Identity Management database:

* **User** - Any signed up user able to identify themselves with an eMail and password. Users can be assigned
 rights individually or as a group
* **Application** -  Any securable FIWARE application consisting of a series of microservices
* **Organization** - A group of users who can be assigned a series of rights. Altering the rights of the organization
 effects the access of all users of that organization
* **OrganizationRole** - Users can either be members or admins of an organization - Admins are able to add and remove users
 from their organization, members merely gain the roles and permissions of an organization. This allows each organization
 to be responsible for their members and removes the need for a super-admin to administer all rights
* **Role** - A role is a descriptive bucket for a set of permissions. A role can be assigned to either a single user
 or an organization. A signed-in user gains all the permissions from all of their own roles plus all of the roles associated
 to their organization
* **Permission** - An ability to do something on a resource within the system

Additionally two further non-human application objects can be secured within a FIWARE application:

* **IoTAgent** - a proxy between IoT Sensors and  the Context Broker
* **PEPProxy** - a middleware for use between generic enablers challenging the rights of a user.


 The relationship between the objects can be seen below - the entities marked in red are used directly within this tutorial:

![](https://fiware.github.io/tutorials.Identity-Management/img/entities.png)

## Video : Introduction to Keyrock

[![](http://img.youtube.com/vi/dHyVTan6bUY/0.jpg)](https://www.youtube.com/watch?v=dHyVTan6bUY "Introduction")

Click on the image above to watch an introductory video describing the **Keyrock** Generic Enabler

# Prerequisites

## Docker

To keep things simple both components will be run using [Docker](https://www.docker.com). **Docker** is a
container technology which allows to different components isolated into their respective environments.

* To install Docker on Windows follow the instructions [here](https://docs.docker.com/docker-for-windows/)
* To install Docker on Mac follow the instructions [here](https://docs.docker.com/docker-for-mac/)
* To install Docker on Linux follow the instructions [here](https://docs.docker.com/install/)

**Docker Compose** is a tool for defining and running multi-container Docker applications. A
[YAML file](https://raw.githubusercontent.com/Fiware/tutorials.Entity-Relationships/master/docker-compose.yml) is used
configure the required services for the application. This means all container services can be brought up in a single
command. Docker Compose is installed by default as part of Docker for Windows and  Docker for Mac, however Linux users
will need to follow the instructions found  [here](https://docs.docker.com/compose/install/)

## Cygwin

We will start up our services using a simple bash script. Windows users should download [cygwin](http://www.cygwin.com/) to provide a
command line functionality similar to a Linux distribution on Windows.

# Architecture

This introduction will only make use of one FIWARE component - the [Keyrock](http://fiware-idm.readthedocs.io/)
Identity Management Generic Enabler. Usage of **Keyrock** alone alone is insufficient for an application to qualify
 as *“Powered by FIWARE”*.  Additionally will be persisting user data in a **MySQL**  database.


The overall architecture will consist of the following elements:

* One **FIWARE Generic Enabler**:
    * FIWARE [Keyrock](http://fiware-idm.readthedocs.io/) offer a complement Identity Management System including:
        * An OAuth2 authentication system for Applications and Users
        * A website graphical front-end for Identity Management Administration
        * An equivalent REST API for Identity Management via HTTP requests

* One [MySQL](https://www.mysql.com/) database :
    * Used to persist user identities, applications, roles and permissions


Since all interactions between the elements are initiated by HTTP requests, the entities can be containerized and run from exposed ports.


![](https://fiware.github.io/tutorials.Identity-Management/img/architecture.png)

The specific architecture of each section of the tutorial is discussed below.

## Keyrock Configuration

```yaml
  keyrock:
    image: fiware/idm
    container_name: fiware-keyrock
    hostname: keyrock
    depends_on:
      - mysql-db
    ports:
      - "3005:3005"
      - "3443:3443"
    environment:
      - DATABASE_HOST=mysql-db
      - IDM_DB_PASS_FILE=/run/secrets/my_secret_data
      - IDM_DB_USER=root
      - IDM_HOST=http://localhost:3005
      - IDM_PORT=3005
      - IDM_HTTPS_ENABLED=true
      - IDM_HTTPS_PORT=3443
      - IDM_ADMIN_USER=admin
      - IDM_ADMIN_EMAIL=admin@test.com
      - IDM_ADMIN_PASS=1234
    secrets:
      - my_secret_data
```

The `idm` container is a web application server listening on two ports:

* Port `3005` has been exposed for HTTP traffic so we can display the web page and interact with the REST API.
* Port `3443` has been exposed for secure HTTPS traffic for the website and REST API

> **Note** HTTPS should be used throughout for any secured application, but to do this properly,
> **Keyrock** requires a trusted SSL certificate - the default certificate is self-certified and
> available for testing purposes. The certificates can be overridden by attaching a volume to
> replace the files under `/opt/fiware-idm/certs`.
>
> In a production environment, all access should occur over HTTPS, to avoid sending
> any sensitive information using plain-text. Alternatively HTTP can be used within a
> private network behind a configured HTTPS Reverse Proxy
>
> The port `3005` offering the HTTP protocol is being exposed for demonstration purposes only and to
> simplify the interactions within this tutorial - you may also use HTTPS on port `3443` with certain
> caveats.
>
> If you want to use HTTPS to access the REST API when you are using Postman, ensure that SSL
> certificate verfication is OFF. If you want to use HTTPS to access the web front-end, please
> accept any security warnings issued.



The `idm` container is driven by environment variables as shown:

| Key |Value|Description|
|-----|-----|-----------|
|IDM_DB_PASS|`idm`| Password of the attached MySQL Database - secured by **Docker Secrets** (see below) |
|IDM_DB_USER|`root`|User name of the default MySQL user - left in plain-text |
|IDM_HOST|`http://localhost:3005`| Host name of the **Keyrock**  App Server - used in activation eMails when signing up users|
|IDM_PORT|`3005`| Port used by the **Keyrock** App Server for HTTP traffic - this has been altered from the default 3000 port to avoid clashes |
|IDM_HTTPS_ENABLED|`true`| Whether to offer HTTPS Support - this will use the self-signed certs unless overridden |
|IDM_HTTPS_PORT|`3443`| Port used by the **Keyrock** App Server for HTTP traffic  this has been altered from the default 443 |


> :information_source: **Note** that this example has secured the MySQL password using **Docker Secrets**
> By using `IDM_DB_PASS` with the `_FILE` suffix and referring to a secrets file location.
> This avoids exposing the password as an `ENV` variable in plain-text - either in the `Dockerfile` Image or
> as an injected variable which could be read using `docker inspect`.
>
> The following list of variables (where used) should be set via secrets with the  `_FILE` suffix  in a Production System:
>
> * `IDM_SESSION_SECRET`
> * `IDM_ENCRYPTION_KEY`
> * `IDM_DB_PASS`
> * `IDM_DB_USER`
> * `IDM_ADMIN_ID`
> * `IDM_ADMIN_USER`
> * `IDM_ADMIN_EMAIL`
> * `IDM_ADMIN_PASS`
> * `IDM_EX_AUTH_DB_USER`
> * `IDM_EX_AUTH_DB_PASS`



## MySQL Configuration

```yaml
  mysql-db:
    image: mysql:5.7
    hostname: mysql-db
    container_name: db-mysql
    expose:
      - "3306"
    ports:
      - "3306:3306"
    networks:
      default:
    environment:
      - "MYSQL_ROOT_PASSWORD_FILE=/run/secrets/my_secret_data"
      - "MYSQL_ROOT_HOST=172.18.1.5"
    volumes:
      - mysql-db:/var/lib/mysql
    secrets:
      - my_secret_data
```


The `mysql-db` container is listening on a single port:

* Port `3306` is the default port for a MySQL server. It has been exposed so you can also run other database tools to display data if you wish

The `mysql-db` container is driven by environment variables as shown:

| Key               |Value.    |Description                               |
|-------------------|----------|------------------------------------------|
|MYSQL_ROOT_PASSWORD|`123`.    | specifies a password that is set for the MySQL `root` account - secured by **Docker Secrets** (see below)|
|MYSQL_ROOT_HOST    |`root`| By default, MySQL creates the `root'@'localhost` account. This account can only be connected to from inside the container. Setting this environment variable allows root connections from other hosts |

# Start Up

To start the installation, do the following:

```console
git clone git@github.com:Fiware/tutorials.Identity-Management.git
cd tutorials.Identity-Management

./services create
```

>**Note** The initial creation of Docker images can take up to three minutes


Thereafter, all services can be initialized from the command line by running the [services](https://github.com/Fiware/tutorials.Identity-Management/blob/master/services) Bash script provided within the repository:

```console
./services <command>
```

Where `<command>` will vary depending upon the exercise we wish to activate.

>:information_source: **Note:** If you want to clean up and start over again you can do so with the following command:
>
>```console
>./services stop
>```
>


### Reading directly from the Keyrock MySQL Database

All Identify Management records  and relationships are held within the the attached MySQL database. This can be
accessed by entering the running Docker container as shown:

```console
docker exec -it db-mysql bash
```

```console
mysql -u <user> -p<password> idm
```

Where `<user>` and `<password>` match the values defined in the `docker-compose` file for `MYSQL_ROOT_PASSWORD`
and `MYSQL_ROOT_USER`. The default values for the tutorial are usually `root` and `secret`.

SQL commands can then be entered from the command line. e.g.:

```SQL
select id, username, email, password from user;
```


### UUIDs within Keyrock

All IDs and tokens within  **Keyrock** are subject to change. The following values will need to be amended when
querying for records. Record IDs use Universally Unique Identifiers - UUIDs.

| Key |Description                        | Sample Value |
|-----|-----------------------------------|--------------|
|`keyrock`| URL for the location of the **Keyrock** service|`localhost:3005`|
|`X-Auth-token`| Token received in the Header when logging in as a user - in other words *"Who am I?"* |`51f2e380-c959-4dee-a0af-380f730137c3`|
|`X-Subject-token`|Token added to requests to define *"Who do I want to inquire about?"* - This can also be a repeat the `X-Auth-token` defined above |`51f2e380-c959-4dee-a0af-380f730137c3`|
|`user-id`| id of an existing user, found with the `user`  table |`96154659-cb3b-4d2d-afef-18d6aec0518e`|
|`organization-id`| id of an existing organization, found with the `organization`  table |`e424ed98-c966-46e3-b161-a165fd31bc01`|
|`organization-role-id`| type of role a user has within an organization either `owner` or `member`|`member`|

Tokens are designed to expire after a set period. If the `X-Auth-token` value you are using has expired, log-in again to obtain a new token.

## Video : Creating User Accounts with the Keyrock GUI

[![](http://img.youtube.com/vi/dtKsjGbJ7Xc/0.jpg)](https://www.youtube.com/watch?v=dtKsjGbJ7Xc " Creating User Accounts")

Click on the image above to watch a video demonstrating how to create users with the **Keyrock** GUI
