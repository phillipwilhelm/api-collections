Welcome to MemberSuite REST & GraphQL API, at membersuite we appreciate the collaboration of third party developers and integrators in our quest to enhance our already comprehensive suite of collaboration products.

# Overview
The Membersuite Engineering Team brings you a comprehensive look at your options of integration with Membersuite. These include GraphQL, REST API options, Single Sign On, and Reverse Single Sign on. 

# Authentication
Details on Authentications using OAuth 2.0 are listed in the Auth Token section. A valid JWT Auth Token is the prerequisite to obtain any data via REST or GraphQL

# GraphQL
The most commonly used GraphQL queries are listed in this documentation for your reference. The beauty of GraphQL is being able to pull exactly the data you want no more, no less, and if you change your mind down the road the data should be easily retrievable.

# REST API Services
In cases, where there is more data to be had or full objects that are needed we also have the option to query using MSQL to our REST service. You will also have the option to call basic CRUD calls for much of the important information that you need.

# Single Sign On
Single Sign On integrators will want to peruse this area of the documentation for specific instructions and calls related to SSO along with the aforementioned OAuth 2 jwt token generation.

# JWT SSO - NEW !
Support for OAuth 2 token SSO is here ! New and Improved ! No need to use SOAP token generation any longer. 
The JWT SSO call will be listed in this area. A cURL will be provided for testing. Once you are done you be able to generate a url that will allow you to login seamlessly into the portal. Note: turn off automatic redirects and look in the location response header for the url. Also, keep in mind that the status code of succes is 302.

Userpool, TenantId, and ClientId will have to be requested of an administrator in order to generate a valid token for your user if you want to integrate a third party CMS. 
The username, password, user pool, and client id of a current user will generate the token needed to pass to the JWTSSO/*TenantId* endpoint to generate your login url programmatically. 

# Reverse SSO

	Reverse SSO (Start on MS, Go To Third Party Site)
+ User is sent from MS to website with 'TokenGUID' query string parameter
+ Third party hits REST API endpoint "GET regularSSO" with TokenGUID and PartitionKey as query string parameters (https://rest.membersuite.com/platform/swagger/ui/index#!/AuthToken/AuthToken_Get)
+ Valid TokenGUID will return Token String value
+ Third party uses Token String value as Authorization Header when hitting REST API endpoint "GET whoAmI" (https://rest.membersuite.com/platform/swagger/ui/index#!/WhoAmI/WhoAmI_Get
+ Valid GET call will return information about the Portal User that generated the original Token String
+ Token String should use "AuthToken" schema, which should be included when using the swagger (i.e. Authorization : AuthToken SyDFOuX+t35sksGHnswBHbB...)
+ Third party uses info returned from "GET whoAmI" (Individual GUID) to create SOAP API search in order to return the required criteria for Third party access privileges
+ Searches can be built using our SOAP API SDKs, .NET and PHP supported (https://github.com/membersuite)
+ AssociationID, PartitionKey, AccessKeyID, & SecretAccessKey are the pieces needed for this implementation. If the Third party needs to generate Tokens (for SSO functionality into MemberSuite), the SigningCertificateID and SigningCertificate.XML file is also required.

# Refer to RegularSSO Post for generation of Token Guids

# Another Method
+	Navigate to an Individual 360 within the MemberSuite Console
+	Under the Security and Auditing Tab, there is a section called "What would you like to do?
+	Under this section, click "Log into MRP as this User"
+	A URL should show up in the address bar that looks similar to this: "https://xxxxx.users.membersuite.com/auth/sso?tokenGUID=00d9c818-3306-4eb8-8855-29a0ddd946a4&nextUrl=&returnText=&logoutUrl="

*	The tokenGUID query string value within this URL is a valid TokenGUID for the user that you attempted to log in as. Please note, this token GUID is only valid for 5 minutes. Any longer and you'll have to generate a new value following these same steps.

	
# Reset Password SSO
As part of your SSO solution you may want to redirect users in a RESET REQUIRED status to the reset password page. For that you need to refer to the Reset Password SSO sample call. YOU WILL REQUIRE THE ASSOCIATION ID of your Association from MemberSuite.
This call allows you to pass:
+ NextUrl which will be automatically redirected to after a user goes through the reset process
+ This nextUrl will be passed the tokenGUID if you wish the user to have single sign on into multiple third party partner sites. 
+ isResetPassword=true or false. If the isResetPassword is set to true the user will be redirected to the Reset page, if the it is set to false the user will be redirected to the forgot password page.

To obtain the appropriate url, make a REST call to the isResetPassword SSO endpoint which is a bit lower down.
The url that is generated from posting nextUrl, isResetPassword, AssociationId, etc. will be in the following format:
* Forgot Password Page
https://xxxxxx.users.membersuite.com/auth/portal-reset-password?nextUrl=aHR0cHM6Ly93d3cubGF0bG1lcy5jb20vYnJlYWtpbmcvYW1hemluZy1uZXctdGVjaC0x&returnText=test&logoutUrl=test
OR
* Reset Password Page
https://xxxxxx.users.membersuite.com/auth/portal-reset-password?isReset=true&nextUrl=aHR0cHM6Ly93d3cubGF0bG1lcy5jb20vYnJlYWtpbmcvYW1hemluZy1uZXctdGVjaC0x&returnText=test&logoutUrl=test

Note: the nextUrl passed will be base 64 encoded and translated by membersuite to redirect the user. 

# Login SSO

As part of your SSO solution you may want to redirect users to the create an account page. For that you need to refer to the isSignUp SSO sample call. YOU WILL REQUIRE THE ASSOCIATION ID of your Association from MemberSuite.
This call allows you to pass:
+ NextUrl which will be automatically redirected to after a user goes through the reset process
+ This nextUrl will be passed the tokenGUID if you wish the user to have single sign on into multiple third party partner sites. 
+ isSignUp=true or false. If the isSignUp is set to true the user will be redirected to the Sign Up Page, if the it is set to false the user will be redirected to the Customizable Sign In page.

To obtain the appropriate url, make a REST call to the isSignUp SSO endpoint which isa bit lower down the page.
The url that is generated from posting nextUrl, isResetPassword, AssociationId, etc. will be in the following format:
* Sign In Page
https://xxxxxx.users.membersuite.com/auth/portal-login?nextUrl=aHR0cHM6Ly93d3cubGF0bG1lcy5jb20vYnJlYWtpbmcvYW1hemluZy1uZXctdGVjaC0x&returnText=test&logoutUrl=test
OR
* Sign Up Page
https://xxxxxx.users.membersuite.com/auth/portal-login?isSignUp=true&nextUrl=aHR0cHM6Ly93d3cubGF0bG1lcy5jb20vYnJlYWtpbmcvYW1hemluZy1uZXctdGVjaC0x&returnText=test&logoutUrl=test

Note: the nextUrl passed will be base 64 encoded and translated by membersuite to redirect the user.

# Profile Retrieval

Steps:
* Obtain valid jwt token using username, password, clientid, and userpoolId. Look in the # Auth Tokens area for more requests. 
* Make a Graph QL call to Get Profile Details to retrieve the image id, use the association call to retrieve the association id (does not change dynamically and can be hard coded if necessary)
* Finally make a call to Images.membersuite.com using the sample provided below in the Retrieve Profile Image folder

Sample flow listed in Profile Retrieval Folder


