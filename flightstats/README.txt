Following parameters are there : -

Appendix - List of flights containing : -
		 - fs code (fs)
		 - airline name (name)
		 - airline phone number (phoneNumber)

Airports - List of airports containing :-
			- fs code of airport (fs)
			- name of airport (name)
			- city name (city)
			- city code (cityCode)
			- country code (countryCode)
			- country name (countryName)
			- region name (regionName)
            - latitude (latitude)
            - longitude (longitude)

flightStatuses - Containing flight status info

			- Flight Id (flightId)
			- Flight Fs code (carrierFsCode)
			- Departure airport fs code (departureAirportFsCode)
			- Arrival airport fs code (arrivalAirportFsCode)
            - Departure date (departureDate)
            - Arrival date (arrivalDate)
            - Flight Status (status)
            - Operational time of flight (operationalTimes)
            
operationalTimes contains following info :-
	- published departure time provided by airline(publishedDeparture)
	- published arrival time provided by airline(publishedArrival)
	- Actual departure time provided by airline(scheduledGateDeparture)
	- Actual arrival time provided by airline(scheduledGateArrival)
            
flightDurations contains following info :-

	- Total flight time(scheduledBlockMinutes)

airportResources contains following info :-

	- Departure flight terminal (departureTerminal)
	- Arrival flight terminal(arrivalTerminal)