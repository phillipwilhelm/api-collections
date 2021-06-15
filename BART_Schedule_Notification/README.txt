This collection collects information on the upcoming BART trips and travel time to the origin station using the user specified origin and destination stations, starting coordinates, and type of travel (defaults to walking). The collections compiles this information and send a Slack DM to a specified user.

## Collection Private Variables

You will need to acquire a token for authorization with these APIs. The BART public token is prepopulated but subject to change.

- `bartApiKey` - [BART API Website](https://www.bart.gov/schedules/developers/api)
- `mqApiKey` - [MapQuest OpenMap API Key](https://developer.mapquest.com/documentation/)
- `slackMemberID` - Slack Member ID for direct messaging, accessible from profile page in Slack
- `slackToken` - Slack App Token - [Slack Apps](https://api.slack.com/authentication/basics)

## User configurable variables

- `tripStartAddress` - The address the user is leaving from to travel to the origin train station
- `tripEndCoordinates` - The coordinates of the origin station
- `routeType` - defaults to pedestrian. See MapQuest API documentation for other modes
- `originStation` - BART origin station abbreviation
- `destinationStation` - BART destination station abbreviation 

## API Providers

- [BART API](https://www.bart.gov/schedules/developers/api)
- [MapQuest Directions API](https://developer.mapquest.com/documentation/open/directions-api/)
- [Slack API](https://api.slack.com/)