This is a work in progress on Candy simply-Fi. It basically works but may need some customization for the commands specific to some devices (most for now). Please feel free to contribute to the api definition, or simply as a tester by using your device with this API definition.

# Candy simply-Fi features

Candy simply-Fi allows you to monitor, get statistics and send some commands to your device when connected to your local network or even from outside your nework.

# How to use this API

## 1. First
* Setup the collection environment variable with your device ip.

## 2. Option a) With Candy ecosystem compatibility
 * Download the official Candy simply-Fi Android app. Register an account and your device. This is required to properly connect the device to your wifi network for now.
 * Setup the collection environment variable with your username/password, device ip / MAC address.
 * Get an auth token (you will have to do that frequently as it expires)
 * Call Remote/Appliance/GetAppliance and retrieve your newly created appliance id and encryption key for this device. Update collection environment variable with these information.

## 2. Option b) Without Candy ecosystem compatibility, local call only
 * Setup the collection environment variable with your WIFI connection details. Be sure to have a DHCP server.
 * Direct connect to the device Wifi AP. This may not work for some devices that requires first peering through Bluetooth and not Wifi AP, for thoses you have to use Option a) for now. For the others you can then call Local Enrollment API.
 
## 3.  Then
 * From there you have no need for the device to be connected to the internet anymore, only to your local network but you have two choices:
	* If you keep internet connection then from outside (or inside) your network you can use Remote API to retrieve statistics or send commands to your device (Candy server act as a proxy / cache server).
	* If you want to directly communicate with the device (recommended, even the official app do that if on the same network), use Local APIs.

# Side notes
 * Candy devices looks to send some UDP broadcast. Such feature may be interesting when not using the remote API at all for device discovery.
 * Is it based on Espressif ESP32? We may have some interesting hacks to perform to access unexposed sensors...
 * The encryption key security is really poor. Simple XOR without any random seed... As most call are predectable, we can easily XOR with the data to found out the key value...