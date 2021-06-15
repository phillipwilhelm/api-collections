# Cisco ISE 3.0 ERS REST APIs

## License
[Cisco Sample Code License](https://developer.cisco.com/site/license/cisco-sample-code-license/)


## Status  
These are the status icons for the requests so far.
- ⌗ : must create resources to test  
- 🚧 : incomplete | untested
- 🛑 : unsupported | bug

## Environment Variables
This collection uses environment variables in scripts in the **Tests** tab to store data (`id`, `name`, `portalId`, etc.)  between requests. This allows you to `GET` or `POST` then immediately `GET {id}` on a resource. Using **No Environment** will cause this convenience functionality to fail so be sure to choose one.


## Collection Variables 
This collection includes some default variables that you will want to update or override with environment variables for your ISE deployment. Specifically, you will want to set: 
- `ise_pan`: the ISE PAN node name or IP address. Default: `ise.securitydemo.net`
- `rest_username`: the username for ERS API access. Must be a member of **SuperAdmin**, **ERSAdmin** or **ERSOperator** groups. Default: `admin` which is the ISE SuperAdmin
- `rest_password`: Default: `C1sco12345`
If you want to manipulate the `guestuser` resource(s) you will also need to use a separate sponsor account specified with:
- `guestuser_username`: Default: `guestapi`
- `guestuser_password`: Default: `C1sco12345`