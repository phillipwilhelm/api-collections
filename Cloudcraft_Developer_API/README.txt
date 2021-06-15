Visualize your cloud architecture with [Cloudcraft, the best way to create smart AWS diagrams](https://www.cloudcraft.co/).

The Cloudcraft API provides programmatic access to and remote rendering of your architecture diagrams. The API also provides fully automated visualization of AWS accounts that are linked with your Cloudcraft account, either as ready to use images or as JSON data.

Use case examples:

- Snapshot and visually compare your live AWS environment state before and after a deployment, from the command line or as part of your automated CI pipeline.
- Download an inventory of all your AWS resources from a linked account as JSON.
- Write a converter from a third party data format to Cloudcraft diagrams.
- Backup, export & import your Cloudcraft data.

Access to the Cloudcraft API requires a [Cloudcraft](https://www.cloudcraft.co/) user account.

Authentication
==============

Your Cloudcraft account is authenticated for the API by including your secret key in the requests. API keys are created in the [Cloudcraft application](https://app.cloudcraft.co/) using the _Manage API keys_ → _Create API Key_ menu option.

<img src="https://static.cloudcraft.co/docs/apikeys.png" alt="Creating API keys" title="Creating API keys" />

An API key provides access to your diagrams and linked AWS accounts, in either read or read-write mode, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, etc.

Authentication to the API is performed via the _Bearer Authorization_ header over HTTPS. For example, using cURL an authorized request looks like this:

```
curl -X GET \
  -H 'Authorization: Bearer eOulZ3vFUUkgfzoBK+UKyPmZw1NsdfrFzdvZoyFJwe8=' \
  https://api.cloudcraft.co/user/me
```

Endpoints
=========

The Cloudcraft API endpoint is **[https://api.cloudcraft.co](https://api.cloudcraft.co)**. For access to the Cloudcraft US GovCloud API, please contact Cloudcraft support.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail.

