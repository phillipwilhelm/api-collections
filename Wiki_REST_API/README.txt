# Introduction
WIKI REST API in order to create a web service to serve WIKI Pages


# Overview
- Using NodeJS for backend development
- Express.js module to handle user requests
- Using mongoose module for MongoDB

Module Dependencies:
- "body-parser": "^1.19.0",
- "ejs": "^2.6.2",
- "express": "^4.17.1",
- "mongoose": "^5.6.6"

Requires Node
- In order to install Node, please follow the instucrions in https://nodejs.org/en/download/

Requires MongoDB
- In order to run your MongoDB server simply type 'mongod' command in your terminal
  - To install MongoDB to your computer please follow the instructions in https://docs.mongodb.com/manual/installation/

API Methods Usage:
- Non-Specific Article CRUD: In order to access this method the following URL standart should be followed 'localhost:3000/articles'
  - GET: Returns all of the articles in JSON format
  - POST: Requires 2 request body components as keys
    - title
    - content
  - DELETE: Deletes all articles in the database
- Specific Article CRUD: In order to access this method the following URL standart should be followed 'localhost:3000/articles/articleTitle'
  - If you'd like to update the articles title and content PUT method is advised, otherwise use PATCH method to update one
  - GET: Returns a spefic article in JSON format
  - PUT: Updates the specific article, requires 2 request body components as keys
    - title: Will be updated
    - content: Will be updated
  - PATCH: Updates the specific article, requires at least one request component. The component sent will be updated
    - title: Will be updated if sent
    - content: Will be updated if sent
  - DELETE: Deletes the specific article. Requires the following request body as key
    - title
- If the title you are using has space in it then place '%20' between the words, for other special characters please follow the instructions in https://www.w3schools.com/tags/ref_urlencode.asp
    
NOTE: Application uses port 3000 unless specified otherwise by the environment variables

# Authentication
None


# Rate limit
One request per user