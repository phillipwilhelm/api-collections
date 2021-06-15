PingOne is a cloud-based identity as a service (IDaaS) framework for secure identity access management. The PingOne API gives developers the tools to manage users and integrate enterprise and third-party applications with the PingOne identity and application management platform.

This document describes the PingOne Management API services, which are used to manage your organization's users and applications, and the Authentication API services, which are used to manage authorization, authentication, permissions, and the sign-on policies that grant users access to applications.

The PingOne APIs manage access to your organization's applications and ensure that only authorized users (your customers, employees, and partners) have access to the applications they have permission to use.


## API endpoints

The PingOne API includes the following public endpoints:

* `api.pingone.com`, `api.pingone.eu`, and `api.pingone.asia`

  These are the primary endpoints for calling PingOne Management API services, with `api.pingone.com` as the public endpoint for calling PingOne API services for environments in the North America region, `api.pingone.eu` as the public endpoint for environments in the European Union region, and `api.pingone.asia` as the public endpoint for environments in the Asia-Pacific region. You can use these endpoints to map requests to directory, application management, and user management resources. For more information about the PingOne Management API model and supported endpoints, see [Management APIs overview](#management-apis).

* `auth.pingone.com`, `auth.pingone.eu`, and `auth.pingone.asia`

  This is the authorization and authentication endpoint called to request the access token required to authenticate PingOne API requests, with `auth.pingone.com` as the public endpoint for calling PingOne Authentication API services for environments in the North America region, `auth.pingone.eu` as the public endpoint for the European Union region, and `auth.pingone.asia` as the public endpoint for the Asia-Pacific region. For more information about the PingOne Authentication API model and supported endpoints, see [Authentication APIs overview](#authentication-apis).



For additional hands-on experience with PingOne platform API endpoints, see [Sample applications](#sample-applications) and [Postman collections](#postman-collection). In the *PingOne API postman collections* section, click the **Run in Postman** button to download a comprehensive Postman collection that includes all PingOne Authentication and Management API endpoints.

For additional information about PingOne authorization and authentication, see [Authentication workflow walkthrough](#authentication-workflow-walkthrough) and [Authorization and authentication by application type](#authorization-and-authentication-by-application-type).

