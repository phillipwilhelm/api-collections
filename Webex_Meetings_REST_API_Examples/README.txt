The new Webex Meetings REST API enables seamless integration of Cisco Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more. Check the [Webex Meetings REST API guide](https://developer.webex.com/docs/api/guides/webex-meetings-rest-api) for more information

The tests in this collection exercise the /meetings API and validate the results.  They are designed to provide developers who are unfamilar with the Meetings API with a set of examples to understand the basic concepts of how to use them. 

1) Create a non recurring meeting tommorow and verify it is gettable
2) Create a recurring meeting starting tommorow recurring daily for 10 instances, and verify it is gettable
3) Create a second non recurring meeting tommorow and modify some of its attributes

Before running these tests the following environment variables must be set:
* WEBEX_TOKEN -- an OAuth token for a user configured for meetings in the test environment. These tests require a token with all the meetings scopes and the spark:people_read scopy.  To get started quickly, developers can copy their temporary token from the [Webex For Developers Gettings Started Guide](https://developer.webex.com/docs/api/getting-started#accounts-and-authentication). 
* MEETINGS_API_URL -- the URL of the meetings API under test, generally the default value of "https://webexapis.com/v1/" does not need to be changed
* TIMEZONE_STRING -- the [Time Zone String](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) that you want your results to be returned in (ie: "America/New_York" for the US East Coast)
* UTCOFFSET - the [offset from UTC Time](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) to set your meetings (ie: "-04:00" for New York during Daylight Savings Time).   This is used by the tests pre-request scripts to create start and end time parameters that will make sense in your timezone
* OTHER_USERS_EMAIL -- an email of another CI user to invite to a meeting.  This user must belong to the same org as the caller of the APIs in order for the PUT /meetingInvitees sample to work.

Pre set:
* MAX_RESULTS -- the max number of meetings to query for -- initially set to 2





