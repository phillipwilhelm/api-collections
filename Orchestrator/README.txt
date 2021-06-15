#### What is this?
A collection of (what we think are) the most useful API calls for UiPath Orchestrator.

#### How does it work?

Just [create a Postman environment](https://learning.getpostman.com/docs/postman/environments_and_globals/manage_environments/#creating-a-new-environment) with the following variables and start making calls.

**For Cloud Orchestrator:**

| Variable | Value |
| ------ | ------ |
| url | [https://platform.uipath.com](https://platform.uipath.com)/[Account Name]/[Tenant Logical Name] |
| userKey | [your User Key] |
| clientId | [your Client ID] |
| (Optional) folderId | [a folder/org unit ID] |

**For On-Premise Orchestrator:**

| Variable | Value |
| ------ | ------ |
| url | [your Orchestrator URL] |
| tenantName | [your Tenant] |
| usernameOrEmailAddress | [your Username] |
| password | [your Password] |
| (Optional) folderId | [a folder/org unit ID] |

_* Notice that the folderId variable is optional. If none is provided, your first Folder/Organization Unit will be used. This is usually named Default._

#### What about  Authentication and Token Refreshing??

Don't sweat it. This collection uses those environment variables to take care of it all automatically in the background. Just press send and your calls will go through without a problem ;)