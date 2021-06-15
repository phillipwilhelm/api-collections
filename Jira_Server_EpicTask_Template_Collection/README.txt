The Postman Collections serve as a template which demonstrates a number of ways to post both issue types, links and field type values to Jira Server using Epics and Epic Links; 
If you find any issues, want to request Readme updates etc please dont hesitate to check out the Github Repo:
https://github.com/Airsickmammal/Jira-Server-Epic-Task-Repeatable-Template-Collections-for-Postman 

You can also find me on Linkedin: https://www.linkedin.com/in/chris-pendlebury/, Twitter, Twitch, Postman and Github under username "Airsickmammal". 
Always happy to hear from and collaborate with the community.

----------------

For Jira Server use REST API version 2 (already in the URLs within this collection). 

To use the API you will need collaborative rights to any target Jira projects.

Use basic Authentication on the "Authorization" tab (above), input your basic username and password. 

EPIC and Task Jira issue types must be enabled within your project to work with the vanilla postman collection.
Epic Name, Epic Link are required fields within your project. Epic Name being specific to the EPIC issue type.

2 ways to get the custom field number for Epic Name and Epic Link: 
1) Go to your global settings, Custom Fields, select Epic Name field, the url will contain "customFieldid=#####" you need to update in the json file. 
2) Use rest API to find the required field(s). You can find this under the "queries" folder or simply note down a Jira issue reference which contains the fields you need, and replace [Jira Host] and [ABC-1] with yours (minus the square brackets):
https://[Jira Host]/rest/api/2/search?jql=key=[ABC-1]

---------------------
PLEASE NOTE - in the API POST calls i have included a few notes, prefixed with "--", you need to remove these when you try to send the POST or it will fail, these are just to instruct with your first time using the template.
---------------------

Fill in the following Variables (see above Variables Tab)
* EPIC REF - Reference for your Epic (e.g. ABC)
* EPIC NAME - Summary/Title for your Epic
* Reporter
* Assignee
* Project Key - Key of your project that normally forms the pre-fix (e.g Issues ABC-1, ABC-2, your Project Key is ABC)
* Jira Host - Your Jira Server URL e.g. jira.Host.com
* Version - Use the version GET in Queries folder to obtain the version Name if you choose to use this
* Impact Name - Create an Array or List field to use this, exampls shows how to enter in a value, this could be a component, or a client's name, whatever your impact name list is defined with
* Due Date - Due date of the issue if you choose to use this, must be in Jira date format e.g. 2020-06-20T00:00:00.000+0100

These fields auto populate
* EPIC KEY - Populates with the issue Key of the epic (e.g. ABC-1) using a "test" after the API call has run
* Task 2 Key, and Task 3 Key: Used in the Vanilla collection to populate with the "2) Task With 2 Sub-Tasks" and "3) Task With Issue Link" issue keys, for use with updating ticket links in API call steps 4) and 5)
To see the "test" which auto populates the values go to either API calls 1), 2) or 3) and select the "Tests" tab