![test](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/postman.jpg)

# Description

This collection shows how to execute data driven execution without using data file. Here we use Google sheet to drive our execution. we are accessing Google sheet through Google sheet API

# Usage instruction

**Google sheet Authorization:**

**Step 1.**
Create google sheet at : https://docs.google.com/spreadsheets/u/0/

**Step 2.**
Copy the sheet id (shown as highlighted)
https://docs.google.com/spreadsheets/d/`1OllrvY6KCOR1GbByUBNCDPR6ikRzuWcODN6fRLgaWFw`/edit#gid=1386834576

**Step 3**

Goto : https://developers.google.com/sheets/api/quickstart/python 
Click: Enable sheet API
Select : Webbrowser as the app type and set : https://www.example.com as the javascript origin
Click Download client Configuration

**Step 4**

Goto: "Retrieve Google sheet" request's Authorization tab and replace the client id and client secrete ,
Click: Get new token and then use new token. (  allow any authorization by clicking continue any way)
Now you are authorized to *Do get request*

**Now you can Execute the collection**

1. set google sheet content as :


| username | password|expectedusername|
|--|--|--|
| user1 | pass1 | user1|
| user2 | pass2 | user2|
| user3 | pass3 | user3|

2. Execute the collection using newman or collection runner