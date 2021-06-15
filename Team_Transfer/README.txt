# Who this collection is for
Those managing and adminstering Postman teams who are looking to transition Postman assets (collections, environments etc.) from one Postman team to another in an automated fashion.

# What does this collection do?
This collection will move a limited set of Postman data (see "What will this do") from one Postman team to another. 

# Setup
Retrieve a Postman API key for both the old and new teams. Add these keys to environment variables `oldTeamAPIKey` and `newTeamAPIKey` as appropriate.

# Running
Run this collection in the collection runner with an environment as described above. **Set a delay between requests of 1000ms** to prevent being rate-limited on the Postman API.

**Be warned**: Once you set this running through the Runner, it's not going to stop until all resources have been copied. If you have a large team, this will take some time. There is no undo with this tool, so be ready to pause the collection run if you spot anything fishy, and be aware that corrections will be manual.

# What this will do
Transfer:
- Workspaces
- Collections
- Environments
- Mocks
- Monitors

# What this won't do
- Move users
- Move history (request runs, monitor results)
- Transfer content you won't see e.g. a private workspace you are not a part of
- Persist any integrations you've setup previously

## Collections
- Persist the roles you have setup currently (viewer/editor)
- Republish public documentation attached to a collection

## Environments
- Transfer the `current value` (e.g. potential secrets), only `intial value`
- Persist user permissioning/defined roles

## Mocks
- All new mocks will be public, so need to be removed/recreated if private

## Monitors
- Integrations will no longer be attached and will need setting up again
- Regions will not be persisted
- Options will not be persisted (disable SSL etc)
- Email notification settings will not be persisted

## APIs
- APIs cannot be handled via Postman API currently and need to be recreated manually

# Other things to consider
Everything will be created as a new entity within the new team. There is no link to the previous content e.g. monitor run results. You will need to update external dependencies appropriately e.g. Newman runs in your CI pipeline.

# Key
- [O]: a request against the old team
- [N]: a request against the new team