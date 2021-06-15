## Cisco Intersight Postman Collection

The Cisco Intersight Postman Collection provides a subset of all Intersight calls. Cisco Intersight is based on the OpenAPI specification and as such a Postman collection can be created directly from the OpenAPI specification.

However the OpenAPI specification does not provide the pre-requestion operation of siging the request.  A request signed with the user's API Key ID and their Secret Key is needed to authenticate the request.  Additionally, the pre-request script pre-processes the Body and URL Postman variable prior to signing the request.

The pre-request script requires two variables, that must be in the current Postman environment and named exactly as follows;

**api-key** - which is available in the Intersight Web interafce after a successful API Key creation.
**secret-key** - which is the complete text of the SecretKet.txt file that is downloaded after a successful API Key creation.

With defined API Key environment variables the provided calls will work within the limits of your Intersight account. With respect to licensing and account capabilities.

The collection also contains some basic test that determine the success or failure of the request and is the request completed in a certain amount of time.

Several of the requests contain post-request tests to perform various activities

- Update the Postman console
- Set Environment variables
- Unset Environment variables

Cisco DevNet provides several Learning Labs and an Inersight Sandbox to get you started using these Postman Calls.

## Cisco DevNet resources

- [Cisco Intersight DevNet Learning Labs ](https://developer.cisco.com/learning/modules/intersight-rest-api)

- [Cisco Intersight DevNet Sandbox](https://devnetsandbox.cisco.com/RM/Diagram/Index/a63216d2-e891-4856-9f27-309ca61ec862?diagramType=Topology)