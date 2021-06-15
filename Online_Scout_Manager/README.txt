Online Scout Manager is a highly useful set of tools provided by Online Youth Manager.

With API Access, you can do so much more with your data. However, there is no documentation for the API and is provided "as-is". This will hopefully help bridge some of that documentation gap.

# Overview
**This is a community documentation project and is not supported or endorsed by Online Youth Manager** (the company responsible for Online Scout Manager). This doumentation is intended for use by existing OSM Customers with an API key (available on request from OYM) to enable creation of their own automated processes.

This documentation project is provided as a guide to the API calls and is created by parties interested in the use of OSM API for automating workloads. If you are looking for code examples, this is not the place for them. Please visit the OSM Forum and navigate to the relevant subforum.

The OSM API itself is not supported and is subject to change at any time. Please use this documentation as a guide only.

# Authentication
To obtain access via API you will first need to request an API key from OSM Support. Simply login to OSM and then navigate to the forum (www.onlinescoutmanager.co.uk/forum).

When you receive your API key, you will need to set up access for it in Settings >> External Access. If you don't allow the key access to something, its relevant API Calls will not work and won't tell you why.

You will need 4 values sending with your header for all POST requests. These are:

#### Secret Key
All requests need a Secret Key. You will get this by running Authenticate User for the first time using your API Key, your API ID, your Email and your Password. 

The result will return your Secret Key and User ID. These will replace your Email and Password in future POST requests.

#### User ID
Obtain this with your Secret Key by Authenticating User. You can also find this in OSM if you read the Members List information. It's your OSM Scout ID.

#### Token
This is your API Key provided to you by Support.

#### API ID
This is the ID for your API Key, also provided to you by Support.


# Gotchas
When writing your automation, there are some things that we have found that would be great to pass on to you, dear developer...

#### White Space
When you are using the API you might want to add little things like trimming to your calls (as the DB stores trailling white spaces to things like Scout Names).

#### Section IDs
Get your Section ID's first, maybe store them somewhere as a KV pair - it gets very annoying to try and work out your SectionID as it's needed pretty much everywhere.

#### OSM Access
Don't forget to give your API Access key the right level of access in OSM. If you have not, for instance, provided even Read Only access to Programmes then you will get a 403 error with no further information when trying to run a query. It will return 'false' to some calls.

# Rate limit
There is a limit to flooding the service, set by OSM. Try to be careful with your requests.

# Lockout
If you post too many 4xx errors (it's easy to do as the interface doesn't give you much feedback) it's very possibly you will get your API key locked. Be careful and verify your parameters against those you are supposed to be sending.

We are told that you will need to leave the API untouched for over 15 mins once you are blocked, any time you try to access with your key while its locked will get your block extended.

Maybe go make a cup of tea and fume silently into it while you think about what might be wrong.

# Contribution
If you wish to contribute to the project, please contact the project creator.

# Restrictions
We are currently restricted to 25 documented calls on the free version of Postman. We will have to make some hard choices what to do about this soon. Watch this space.