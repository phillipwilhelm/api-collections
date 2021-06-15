The tutorial explains how to create applications, and how to assign roles and permissions to them.
It takes the users and organizations created in the [previous tutorial](https://github.com/Fiware/tutorials.Identity-Management)
and ensures that only legitmate users will have access to resources.

The `docker-compose` files for this tutorial can be found on GitHub: 

![GitHub](https://fiware.github.io/tutorials.Identity-Management/icon/GitHub-Mark-32px.png) [FIWARE 402: Roles and Permissions](https://github.com/Fiware/tutorials.Roles-Permissions)

# What is Authorization?

> "No matter what he does, every person on earth plays a central role in the history of the world.
> And normally he doesn't know it"
>
> — Paulo Coelho (The Alchemist)


Authorization is the function of specifying access rights/privileges to resources related to information
security. More formally, "to authorize" is to define an access policy. In the case of Keyrock, User
access is granted based on permissions assigned to a role.

Every application secured by the **Keyrock** generic enabler can define a set of permissions - i.e.
a set of things that can be done within the application. For example within the application, the ability
to send a commmand to unlock a Smart Door could be secured behind a `Unlock Door` permission. Similarly
the ability to send a commmand to ring the alarm bell could be secured behind a `Ring Bell` permission,
and the ability to alter prices could be secured behind a `Price Change` permission

These permissions are grouped together in a series of roles - for example `Unlock Door` and `Ring Bell`
could both be assigned to the Security Role, meaning that Users who are subsequently given that role
would gain both permissions.

Permissions can overlap and be assigned to multiple roles - maybe `Ring Bell` is also assigned to the management
role along with `Price Change` and `Order Stock`.

In turn users or organizations will be assigned to one of more roles - each user will gain the sum of all the
permissions for each role they have. For example if Alice is assigned to both management and security roles,
she will gain all four permissions `Unlock Door`, `Ring Bell`, `Price Change` and `Order Stock`.

The concept of a role is unknown to a user - they only know the list of permissions they have been granted,
not how the permissions are split up within the application.

In summary, permissions are all the possible actions that can be done to resources within an application, whereas roles
are groups of actions which can be done by a type of user of that application.


## Standard Concepts of Identity Management

The following common objects are found with the **Keyrock** Identity Management database:

* **User** - Any signed up user able to identify themselves with an eMail and password. Users can be assigned
 rights individually or as a group
* **Application** -  Any securable FIWARE application consisting of a series of microservices
* **Organization** - A group of users who can be assigned a series of rights. Altering the rights of the organization
 effects the access of all users of that organization
* **OrganizationRole** - Users can either be members or admins of an organization - Admins are able to add and remove users
 from their organization, members merely gain the roles and permissions of an organiation. This allows each organization
 to be responisible for their members and removes the need for a super-admin to administer all rights
* **Role** - A role is a descriptive bucket for a set of permissions. A role can be assigned to either a single user
 or an organization. A signed-in user gains all the permissions from all of their own roles plus all of the roles associated
 to their organization
* **Permission** - An ability to do something on a resource within the system

Additionally two further non-human application objects can be secured within a FIWARE application:

* **IoTAgent** - a proxy betwen IoT Sensors and  the Context Broker
* **PEPProxy** - a middleware for use between generic enablers challenging the rights of a user.


 The relationship between the objects can be seen below:

![](https://fiware.github.io/tutorials.Roles-Permissions/img/entities.png)

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
    * Used to persist user identities, applications, roles and permsissions


Since all interactions between the elements are initiated by HTTP requests, the entities can be containerized and run from exposed ports.


![](https://fiware.github.io/tutorials.Roles-Permissions/img/architecture.png)

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
      - DEBUG=idm:*
      - DATABASE_HOST=mysql-db
      - IDM_DB_PASS_FILE=/run/secrets/my_secret_data
      - IDM_DB_USER=root
      - IDM_HOST=http://localhost:3005
      - IDM_PORT=3005
      - IDM_HTTPS_ENABLED=true
      - IDM_HTTPS_PORT=3443
      - IDM_ADMIN_USER=alice
      - IDM_ADMIN_EMAIL=alice-the-admin@test.com
      - IDM_ADMIN_PASS=test
    secrets:
      - my_secret_data
```

The `keyrock` container is a web application server listening on two ports:

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



The `keyrock` container is driven by environment variables as shown:

| Key |Value|Description|
|-----|-----|-----------|
|IDM_DB_PASS|`idm`| Password of the attached MySQL Database - secured by **Docker Secrets** (see below) |
|IDM_DB_USER|`root`|User name of the default MySQL user - left in plain-text |
|IDM_HOST|`http://localhost:3005`| Host name of the **Keyrock**  App Server - used in activation eMails when signing up users|
|IDM_PORT|`3005`| Port used by the **Keyrock** App Server for HTTP traffic - this has been altered from the default 3000 port to avoid clashes |
|IDM_HTTPS_ENABLED|`true`| Whether to offer HTTPS Support - this will use the self-signed certs unless overridden |
|IDM_HTTPS_PORT|`3443`| Port used by the **Keyrock** App Server for HTTP traffic  this has been altered from the default 443 |


> **Note** that this example has secured the MySQL password using **Docker Secrets**
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
git clone git@github.com:Fiware/tutorials.Roles-Permissions.git
cd tutorials.Roles-Permissions

./services create
```

>**Note** The initial creation of Docker images can take up to three minutes


Thereafter, all services can be initialized from the command line by running the [services](https://github.com/Fiware/tutorials.Roles-Permissions/blob/master/services) Bash script provided within the repository:

```console
./services <command>
```

Where `<command>` will vary depending upon the exercise we wish to activate.

> **Note:** If you want to clean up and start over again you can do so with the following command:
>
>```console
>./services stop
>```
>


### Dramatis Personae

The following people at `test.com` legitimately have accounts within the Application

* Alice, she will be the Administrator of the **Keyrock** Application
* Bob, the Regional Manager of the supermarket chain - he has several store managers under him:
  * Manager1
  * Manager2
* Charlie, the Head of Security of the supermarket chain - he has several store detectives under him:
  * Detective1
  * Detective2

The following people at `example.com`  have signed up for accounts, but have no reason to be granted access

* Eve - Eve the Eavesdropper
* Mallory - Mallory the malicious attacker
* Rob - Rob the Robber


| Name       |eMail                       |Password | UUID                                  |
|------------|----------------------------|---------|---------------------------------------|
| alice      | alice-the-admin@test.com   | `test`  |`aaaaaaaa-good-0000-0000-000000000000` |
| bob        | bob-the-manager@test.com   | `test`  |`bbbbbbbb-good-0000-0000-000000000000` |
| charlie    | charlie-security@test.com  | `test`  |`cccccccc-good-0000-0000-000000000000` |
| manager1   | manager1@test.com          | `test`  |`manager1-good-0000-0000-000000000000` |
| manager2   | manager2@test.com          | `test`  |`manager2-good-0000-0000-000000000000` |
| detective1 | detective1@test.com        | `test`  |`secure01-good-0000-0000-000000000000` |
| detective2 | detective2@test.com        | `test`  |`secure02-good-0000-0000-000000000000` |
| eve        | eve@example.com            | `test`  |`eeeeeeee-evil-0000-0000-000000000000` |
| mallory    | mallory@example.com        | `test`  |`mmmmmmmm-evil-0000-0000-000000000000` |
| rob        | rob@example.com            | `test`  |`rrrrrrrr-evil-0000-0000-000000000000` |


Two organizations have also been set up by Alice:

| Name       | Description                         | UUID                                 |
|------------|-------------------------------------|--------------------------------------|
| Security   | Security Group for Store Detectives |`security-team-0000-0000-000000000000`|
| Management | Management Group for Store Managers |`managers-team-0000-0000-000000000000`|

The data creating users and organizations from the [previous tutorial](https://github.com/Fiware/tutorials.Identity-Management) has been downloaded:

```console
docker exec db-mysql /usr/bin/mysqldump -u root --password=idmx idm > backup.sql
```

and is injected into the MySQL Database on start-up.




To refresh your memory about how to create users and organizations, you can log in at `http://localhost:3005/idm`
using the account `alice-the-admin@test.com` with a password of `test`.

![](https://fiware.github.io/tutorials.Roles-Permissions/img/log-in.png)

and look at the organizations list.



### Reading directly from the Keyrock MySQL Database

All Identify Management records  and releationships are held within the the attached MySQL database. This can be
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

All ids and tokens within  **Keyrock** are subject to change. The following values will need to be amended when
querying for records .Record ids use Universally Unique Identifiers - UUIDs.

| Key |Description                        | Sample Value |
|-----|-----------------------------------|--------------|
|`keyrock`| URL for the location of the **Keyrock** service|`localhost:3005`|
|`X-Auth-token`| Token received in the Header when logging in as a user |`aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa` = I am Alice|
|`X-Subject-token`|Token to pass when asking about a subject, alternatively repeat the user token |`bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbb` = Asking about Bob|
|`user-id`| id of an existing user, found with the `user`  table |`bbbbbbbb-good-0000-0000-000000000000` - Bob's User Id|
|`application-id`| id of an existing application, found with the `oauth_client` table |`c978218d-ad63-4427-b12b-542b81299cfb`|
|`role-id`| id of an existing role, found with the `role` table |`d28baa00-839e-4b45-a6b2-1cec563942ee`|
|`permission-id`| id of an existing permission, found with the `permission`  table |`6b6cd19c-9398-4834-9ba1-1616c57139c0`|
|`organization-id`| id of an existing organization, found with the `organization`  table |`e424ed98-c966-46e3-b161-a165fd31bc01`|
|`organization-role-id`| type of role a user has within an organization either `owner` or `member`|`member`|
|`iot-agent-id`| id of an existing IoT Agent, found with the `iot`  table  |`iot_sensor_f3d0245b-3330-4e64-a513-81bf4b0dae64`|
|`pep-proxy-id`| id of an existing PEP Proxy, found with the `pep_proxy`  table  |`iot_sensor_f3d0245b-3330-4e64-a513-81bf4b0dae64`|

Tokens are designed to expire after a set period. If the `X-Auth-token` value you are using has expired, log-in again to obtain a new token. For this tutorial, a long lasting set of tokens has been created for each user and persisted into the database,
so there is usually no need to refresh tokens.