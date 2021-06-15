## Summary
Postman collection implementing proper HMAC authentication to enable ad-hoc testing of the Duo API to make integration with automated security tooling easier for Security Engineers.

As of 07/08/19, The Duo Auth/Admin API use SHA-1 HMAC for their basic authentication. This collection comes with an environment, which has the following fields the user needs to fill out: 

duo-API-HOST: API endpoint\
duo-`(auth|admin)`-skey: Secret key\
duo-`(auth|admin)`-ikey: Integration key

These will not be shared if added to the environment which comes in the collection, but it's probably sensible to create a separate environment and copy the variables over, if it makes you feel better.

## Importing Environment
If you got this collection using the Templates menu, or otherwise need an import copy of the environment, you can find it here:\
\
```
{
	"id": "e0f26d04-60e9-434c-88b9-50e9c7c5393b",
	"name": "Duo API for Postman Environment",
	"values": [
		{
			"key": "auth-ikey",
			"value": "CHANGEME",
			"type": "text",
			"enabled": true
		},
		{
			"key": "auth-skey",
			"value": "CHANGEME",
			"type": "text",
			"enabled": true
		},
		{
			"key": "duo-DATE",
			"value": "",
			"type": "text",
			"enabled": true
		},
		{
			"key": "duo-admin-HMAC",
			"value": "",
			"type": "text",
			"enabled": true
		},
		{
			"key": "duo-API-HOST",
			"value": "CHANGEME",
			"type": "text",
			"enabled": true
		},
		{
			"key": "duo-auth-HMAC",
			"value": "",
			"type": "text",
			"enabled": true
		},
		{
			"key": "admin-ikey\n",
			"value": "CHANGEME",
			"type": "text",
			"enabled": true
		},
		{
			"key": "admin-skey",
			"value": "CHANGEME",
			"type": "text",
			"enabled": true
		}
	],
	"_postman_variable_scope": "environment",
	"_postman_exported_at": "2019-08-07T10:09:28.398Z",
	"_postman_exported_using": "Postman/7.3.6"
}```

Save it to a file (ideally `{environment_name}.postman.json`) and Import by selecting "Manage Environments" -> "Import".

### Note

__It's worth noting that Postman's pre-generated queries on this page will not work because all of the parameters (the URL being sent to, the Authorization header e.t.c.) rely on contextual info which will differ between use-cases. It works, I promise! 😇__