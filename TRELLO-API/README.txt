# Introduction
This API is for manage a MySQL database for TaskManagement and by using Spring Framework especially Spring Data JPA and Spring Data Rest 

# Overview
To use and test this API in development enviroment 

## Date and Time 
 Because the app is intended to be used many user around the world . As a result , all the date and time is stored in the database as UTC timezone

By default createTime of any new entity will be the time that it is created (converted to UTC timezone)

to make a JSON date (for date of birth) the follow format: "yyyy-mm-dd" for example : "1990-02-28"

to make a JSON datetime (for createTime , updateTime , dateStart , dateFinish) the follow format :
"yyy-mm-dd"T"hh-mm-ss" for example : "2019-11-18T09:00:00" . Also please make sure it is converted to UTC time zone

## Request Method:
by default Spring auto generate API can be used with 5 request method :"GET" , "POST" , "PUT" , "PATCH" , "DELETE"

"GET" : to get the data from the database 

"POST" : to make a new entity

"PUT" : to modify all the non-link field (non-relationship column) of the entity

"PATCH" : to modify only the mentioned field (or column). However unlike "PUT" this is the only request Method to update link field (relationship column)

"DELETE" : to delete an entity

## Security
This API will use Spring Security and JSON Web Token with Bearer Schema for security.

Moreover , As Spring Security recommended . The password for each user will use Bcrypt Password Hashing Function. 
However , As a result Bcrypt Password Hashing Function is an one way trip. Meaning the hashed password will be store on the database and there is no way to convert it back to plain text (but there are ways to check plain text and hashed password are the same or not of course)

The JSON Web Tokens that are issued by this API will sometime be warned by some websites that there are asymmetric keys vulnerabilities. However as I am using Java jwt to generate JSON Web Tokens,  they claimed to fix this issue by apply stricter verification for token :  https://github.com/auth0/java-jwt/issues/53 . However I have never tried to hack a token before so this knowledge is beyond my ability to determine.

Currently a token will be valid for a week

## Role
Currently the API only support 2 roles : "ADMIN" and "USER"

To summary the "ADMIN" will have authority like "USER" plus extra authority

The "USER" will have all authority to see everything except to see the reports (future featue) and see other User login details . The User will only have the ability to change their login detail and their Staff detail only (except office assignment)

the "ADMIN" on the other hand will have all the authority below and no restriction. 

I Will mark the authority for each request below


## Hypermedia as the Engine of Application State (HATEOAS)
Because this API is made by mainly using Spring Data Rest and Spring Data JPA . And Spring use HATEOAS as REST application architecture so extra knowledge about HATEOAS is helpfull

## Exception handling 
Only exception related to Database Constraint Violation is handled. Any other exception did not cross my mind so please notify me

## Known Issue
Currently I have no knowledge on how to expire an already issued token sooner than its expiration date.

## Bug and Bugs
This is my first real API project so I do expect there will be a lot of bugs. As a result please notify me