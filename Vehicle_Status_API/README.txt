This API allows to get status information of windows and doors, deck lid, rooftop or sunroof and interior lights of connected Mercedes-Benz vehicles remotely.
Data is categorized into resources and containers for the polling interface. They are defined as follows:
* *Resource*: A resource is a single information about a vehicle. It's a measurement that consists of a name (also referred to as resource ID), a value, and an associated timestamp. See below for a list and description of all resources that this API provides.
* *Container*: A container is a set of resources that are defined to group data for a certain use case.

The interface is a ISO 20078-compliant REST endpoint to query the latest data for a vehicle. If the vehicle did not send an update for a resource within 12 hours, the response will be empty.
## Resources
This is an alphabetical list of all resources that the API provides.
Name | Description | Unit/Range
---- | ----------- | ----------
decklidstatus | Deck lid latch status opened/closed state | false: closed<br>true: open
doorstatusfrontleft | Status of the front left door | false: closed<br>true: open
doorstatusfrontright | Status of the front right door | false: closed<br>true: open
doorstatusrearleft | Status of the rear left door | false: closed<br>true: open
doorstatusrearright | Status of the rear right door | false: closed<br>true: open
interiorLightsFront | Front light inside | false: off<br>true: on
interiorLightsRear | Rear light inside | false: off<br>true: on
lightswitchposition | Rotary light switch position | 0: auto<br>1: headlights<br>2: sidelight left<br> 3: sidelight right<br>4: parking light
readingLampFrontLeft | Front left reading light inside | false: off<br>true: on
readingLampFrontRight | Front right reading light inside | false: off<br>true: on
rooftopstatus | Status of the convertible top opened/closed | 0: unlocked <br>1: open and locked <br>2: closed and locked
sunroofstatus | Status of the sunroof | 0: Tilt/slide sunroof is closed<br>1: Tilt/slide sunroof is complete open<br>2: Lifting roof is open<br>3: Tilt/slide sunroof is running<br>4: Tilt/slide sunroof in anti-booming position<br>5: Sliding roof in intermediate position<br>6: Lifting roof in intermediate position
windowstatusfrontleft | Status of the front left window  | 0: window in intermediate position<br>1: window completely opened<br>2: window completely closed<br>3: window airing position<br>4: window intermediate airing position<br>5: window currently running
windowstatusfrontright | Status of the front right window  | 0: window in intermediate position<br>1: window completely opened<br>2: window completely closed<br>3: window airing position<br>4: window intermediate airing position<br>5: window currently running
windowstatusrearleft | Status of the rear left window  | 0: window in intermediate position<br>1: window completely opened<br>2: window completely closed<br>3: window airing position<br>4: window intermediate airing position<br>5: window currently running
windowstatusrearright | Status of the rear right window | 0: window in intermediate position<br>1: window completely opened<br>2: window completely closed<br>3: window airing position<br>4: window intermediate airing position<br>5: window currently running


Contact Support:
 Name: The open API platform by Mercedes-Benz