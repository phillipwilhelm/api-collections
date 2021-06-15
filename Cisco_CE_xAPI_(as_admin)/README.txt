xAPI is the Application Programming Interface (API) for Collaboration Endpoint software(Cisco CE and RoomOS), for both on-premise registered video conferencing devices (CUCM, VCS) as well as devices registered to Cisco’s cloud service (Cisco Webex Devices).

**This collection gathers commands accessible to an 'Admin' user, and local to the collaboration device.**

Which commands are available depends on the product, the back-end (on-premise, cloud), and the user role of the local user (admin, audit, integrator, roomcontrol, user). To get an overview of the commands, check the reference guide for the version of CE or RoomOS you are running. 
Here is a link to the guide for CE 9.8 and RoomOS as of September 2019: https://www.cisco.com/c/dam/en/us/td/docs/telepresence/endpoint/ce98/collaboration-endpoint-software-api-reference-guide-ce98.pdf

This collection comes with default environment variables:
- endpoint: replace with the LAN ip adress of your collection device, defaults to: http://192.168.1.32
- credentials: replace with your integrator credentials, or one of the proposed below, defaults to: 'creds-admin'
- creds-integrator: defaults to 'aW50ZWdyYXRvcjppbnRlZ3JhdG9y', which corresponds to a base64 encoding of 'integrator:integrator' - the default credentials for the 'Integrator' role on [DevNet Sandbox RoomKit devices](https://github.com/CiscoDevNet/awesome-xapi#developer-tools)
- creds-admin: defaults to 'cmVtb3Rlc3VwcG9ydDo2US82a0JDYnJ0DQo=', which corresponds to a base64 encoding of 'admin:ciscopsdt' - the default credentials for the "Admin" role on [DevNet Sandbox RoomKit devices](https://github.com/CiscoDevNet/awesome-xapi#developer-tools)
- creds-localadmin: defaults to 'bG9jYWxhZG1pbjpjaXNjb3BzZHQ', which corresponds to a base64 encoding of "localadmin:ciscopsdt" - the default credentials for DevNet learning labs when addind an "Admin" role for cloud-registered Webex Devices running RoomOS.