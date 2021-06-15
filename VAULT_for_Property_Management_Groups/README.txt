BluePort Vault is an authentication backend and a Wi-Fi key store used to enable Globally Unique Wi-Fi WPA2 Passphrases for Internet subscribers.

Vault enables single SSID networks for large residential communities with property-wide roaming (yes, even the ones with thousands of residents - and yes, across properties), centralizes key distribution for both large scale enterprise and consumer networks, provides each subscriber with their own encypted key and secures the Wi-Fi transmission. Vault enables Managed Wi-Fi platforms providers to provide multi-venue Wi-Fi services to their customers. ISPs, network operators, and businesses can futher provide Wi-Fi as a service to their members and patrons, using additional Vault services offered through their Managed Wi-Fi platform provider. Whew!

Documentation NOTE: All the API calls for Network Software Providers will be listed at this URL : https://documenter.getpostman.com/view/10711528/Szt5eAUm

Documentation NOTE: All the API calls for Property Management Groups **(this document)** will be listed at this URL : https://documenter.getpostman.com/view/10711528/Szzn6bij


ONBOARDING GUIDE FOR PROPERTY MANAGEMENT GROUPS
-----------------------------------------------

`To consume the following APIs, you will also need an API key from the Vault administrators. Set the API key in header "x-api-key" of API calls. `


**Step 1 - Connect with a Network Operator**

- Call `/propertymanagement/networkoperators/connectWithNetworkOperator` to connect with a Network Operator.
- Your available and in-service venues will be visible to connected Network Operators. 
- Both Network Operators and Property Management Groups can see each other's keypools. 


**Step 2 - Add a venue**

- Call `/propertymanagement/addVenue` to add a new venue
- Call `/propertymanagement/listVenues` to list venues with network operator info and associated keypools

**Step 3 - List network operators**

- Call `/propertymanagement/networkoperators/listNetworkOperators` to get a list of all Network Operators. All Network Operators in the system are visible to Property Management Groups.

**Step 4 - Provide venue access to Network Operator**

- Call `/propertymanagement/networkoperators/assignVenuetoNetworkOperator` to assign a network operator to a venue, or to approve Network Operator's request to service a venue. 
- Call `/propertymanagement/listVenues` to list venues with network operator info and associated keypools

**Step 5 - Add a keypool**

- Call `/propertymanagement/addKeypool` to add a new SSID
- Call `/propertymanagement/listKeypools` to list your keypools and your Network Operator's keypools. 

**Step 6 - Authorize keypool for a venue**

- Call `/propertymanagement/authorizeKeyPoolatVenue` to authorize any of your own keypools to a venue, or to authorize Network Operator's request to their subscribers at your venue. 
- Call `/propertymanagement/listKeypools` to list venue-keypool attachments.

**Step 7 - Add a subscriber**

- Call `/propertymanagement/subscribers/addSubscriber` to add a new subscriber account.
- Note the returned SubscriberToken. You should attach the SubscriberToken to each subscriber account in your system. (e.g. loyalty memebership number or customer's email address). 
- For PII purposes, Vault does not require any other identifier for your subscriber account other than the SubscriberToken. 
- Each subscriberToken can have multiple keys (Wi-Fi WPA2 PSK) attached to their account. 
- To get a list of new SubscriberTokens that do not have a key attached, call  `/propertymanagement/subscribers/listUnusedSubscriberTokens`. You cannot have more than 5 unused unused SubscriberTokens. 

**Step 8 - Add a key**
- Call `/propertymanagement/subscribers/addKey` to add a key (e.g. Wi-Fi WPA2 PSK) for a subscriberToken. 
- Call `/propertymanagement/listKeypools` to view updated list of subscribers for associated KeypoolID
- You can only add keys to keypools that you own.
- Call `/propertymanagement/listVenue` to view updated list of network policies for associated VenueID
- You can only add keys to keypools that you own.

Network Policies 

- You can add network policies for venues that you own to the keypool that you own. 
- Network Operators can add network policies for venues that you own to their keypools. 
- Network Operators cannot add network policies for keypools that you own. 


**Notes for Network Operators**

- To authenticate a subscriber device using the key, set up your Wi-Fi controller to call external RADIUS server for external DPSK. The RADIUS server will require API extensions and will forward incoming authentication request from Wi-Fi controller to Vault. 