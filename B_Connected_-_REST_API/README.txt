This is the documentation of °B Connected's REST API.

# Overview
In terms of security reasons, the REST API provides read requests only. The following requests are provided:
+ **Get Devices** : *Retrieve a list of devices including the devices' meta-data for a given filter*
+ **Get Current Device Temperature** : *Retrieve the current temperature for a device*
+ **Get Device Temperature Hisotry** : *Retrieve the temperature history of a device for a given start and end date*
+ **Get CSF Batches** : *Get a list of batches frozen by a given device within a given time range.*
+ **Get Events** : *Retrieve a list of events of a device for a given filter*
+ **Get Active Alarms** : *Get a list of active alarms*

# Authentication
In order to use the REST API, you need to create an user with API access right. For more information please refer to chapter *12.2 Roles Management* of the user manual.

# Request
The URL to use the REST API with your °B Connected installation composes as follows:

**[http protocol][Server IP or name]/bconnected/[Function]**
<br>Example: http://10.17.10.238/bconnected/api/deviceListByLocationFilter

You can use http or https, depending on your installation. No port has to be specified for the requests.


# Error Codes
Following are the different error codes that may be returned by the API:

<table>
	<tr>
		<td>**Code**</td>
		<td>**Label**</td>
		<td>**Description**</td>
	</tr>
	<tr>
		<td>200</td>
		<td>OK</td>
		<td>Indicates that the client's request way accepted successfully</td>
	</tr>
	<tr>
		<td>500</td>
		<td>Internal Server Error</td>
		<td>Indicates that there is a problem with the server</td>
	</tr>
</table>

# Language support
The API supports multiple languages. The language of the returned values can selected by setting the parameter "lang" in the header of each request. Example: *'lang: en'*. <br>
Here are the supported languages:

<table>
	<tr>
		<td>**Language**</td>
		<td>**Language code**</td>
	</tr>
	<tr>
		<td>English</td>
		<td>en</td>
	</tr>
	<tr>
		<td>French</td>
		<td>fr</td>
	</tr>
	<tr>
		<td>German</td>
		<td>de</td>
	</tr>
</table>

More languages will follow.

# Change log
+ *17.10.2018* : **Creation**
+ *06.12.2018* : **Updates and bug fixes**