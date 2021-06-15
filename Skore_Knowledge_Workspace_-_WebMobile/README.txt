The Skore Knowledge Workspace API provides external access to resources and services, making the platform open and extensible. The API uses REST for all resources.

The list of endpoints are used for WebApps or MobileApps integration and for Machine-to-Machine integrations see more [M2M](https://docs-m2m.skore.io)

You can send the client's metadata in all requests using `Skore-Request-Metadata` header. See all metadata below.

Client metadata sample for all platforms:

Web:

* city - The city of the event sender
* region - The region (state or province) .
* country - The country of the event sender
* app_build_number - General build of this app.
* app_version_string - Current app version.
* browser - Browser name.
* browser_version - Browser version number.
* device - The name of the event sender's device, if they're on mobile web.
* current_url - The full URL of the webpage on which the event is triggered.
* initial_referrer - Referring URL at first arrival.
* initial_referring_domain - Referring domain at first arrival.
* os - OS of the event sender.
* referrer - Referring URL, including your own domain.
* referring_domain - Referring domain, including your own domain.
* screen_height - The height of the screen of the device.
* screen_width - The width of the screen of the device.
* utm_parameters - Any utm tags associated with the link a customer clicked to arrive at your domain. Each utm will be collected under its own property. Mixpanel only tracks first touch UTM parameters by default. 

iOS:

* city - The city of the event sender, parsed from IP.
* region - The region (state or province) of the event sender, parsed from IP.
* country - The country of the event sender, parsed from IP.
* app_build_number - General build of this app.
* app_version_string - Current app version.
* app_flavor - string - app flavor. 
* carrier - Wireless carrier of the device owner.
* os_version - Current version of iOS on the device.
* manufacturer - Always Apple (so far...).
* device_model - Device model ID, in format "iPad 3,4". Full list here.
* os - "iPhone OS" (outdated naming convention).
* radio - Current cellular network communication standard (3G, 4G, LTE, etc).
* screen_height - Height, in points, of the device screen.
* screen_width - Width, in points, of the device screen.
* wifi - Set to true if Wifi is connected, false if not.

Android:

* city - The city of the event sender, parsed from IP. .
* region - The region (state or province) of the event sender, parsed from IP.
* country - The country of the event sender, parsed from IP.
* app_version_string - Current app version.
* app_build_number - General build of this app.
* app_flavor - string - app flavor.
* bluetooth_enabled - Set to true is Bluetooth is enabled, false if not.
* bluetooth_version - Set to "none", "ble", or "classic".
* brand - Device brand.
* carrier - Wireless carrier of the device owner.
* has_nfc - Set to true if Near Field Communication is being used, false if not.
* has_telephone - Set to true if this device has telephone functionality, false if not.
* manufacturer - Device manufacturer.
* device_model - Device model.
* android_os - Android.
* os_version - Current Android version for this device.
* screen_dpi - Pixel density of the device screen.
* screen_height - Height, in pixels, of the device screen.
* screen_width - Width, in pixels, of the device screen.
* wifi - Set to true is Wifi is connected, false if not.
* google_play_services - Verifies that Google Play services is installed and enabled on this device, 
* and that the version installed on this device is no older than the one required by this client.