This API allows access to odometer information data of Mercedes-Benz vehicles to offer distance based insurance services.
Data is categorized into resources and containers for the polling interface. They are defined as follows:
* *Resource*: A resource is a single information about a vehicle. It's a measurement that consists of a name (also referred to as resource ID), a value, and an associated timestamp. See below for a list and description of all resources that this API provides.
* *Container*: A container is a set of resources that are defined to group data for a certain use case.

The interface is a ISO 20078-compliant REST endpoint to query the latest data for a vehicle. If the vehicle did not send an update for a resource within 12 hours, the response will be empty.
## Resources
This is an alphabetical list of all resources that the API provides.
Name | Description | Unit/Range
---- | ----------- | ----------
odo | Odometer | 0..999999 km


Contact Support:
 Name: The open API platform by Mercedes-Benz