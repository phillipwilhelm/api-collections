# Who this collection is for
Security teams who are looking to automate the process of checking for secrets leaking within Postman. Beyond providing education and training, we can continually assess our Postman data all of the time through this powerful collection.

# What does this collection do?
This collection is designed to be setup as a Postman Monitor to scan Postman Environments within Team Workspaces that might be exposing secrets through the initial value field.

# Setup

## Configure the Postman Environment

1) Review the provided `Environment Scanner` Postman Environment. The `regex` field contains key value pairings of a) the type of secret and b) the regex to match such a secret. This should be altered to cover the types of secrets you wish to scan for. We've included a range of popular types of secrets for your convenience.

2) [Create a Postman API key](https://learning.postman.com/docs/postman/postman-api/intro-api/#postman-api-overview) and add this to the `postmanAPIKey` field within the `Enviroment Scanner` Postman Environment. It should sit within both the initial and current value columns.

## Create the Postman Monitor

1) On the imported `Environment Scanner` Postman Collection, go into the Collection menu and select `Monitor Collection`. See [Creating a Monitor](https://learning.postman.com/docs/postman/monitors/setting-up-monitor/) for more help.

2) The `Monitor run frequency` you select will determine how often the collection runs. Once daily is likely fine to begin within.

3) Select `Show additional preferences` and set the `Request delay` to `1000`ms. This is necessary such that we don't get rate limited against the Postman API.

4) You can now hit `Create` and the monitor will execute on the frequency you selected.

## Viewing Results

1) [Our existing documentation](https://learning.postman.com/docs/postman/monitors/viewing-monitor-results/) covers how to view the results of a monitor.

2) You will see that the `Environment Scanner` executes many requests through its collection run. Scroll all the way to the bottom. For each test failure that you see, this indicates a potentially exposed secret. The offending environment's ID, and the exact key containing the secret are provided. In this case, two environments are highlighted, each with a single offending key.

![Monitor results](https://i.imgur.com/foKEz7r.png)

3) Scrolling to the top of the Monitor results, select the `Console Log` tab. Again, scrolling all the way to the bottom, you can find a JSON output of these results:

![Logs](https://i.imgur.com/EVxEuS0.png)

4) To review and correct an enviromnent in question, simply take the Environment ID found in the test failure / the `env` value in the logs, and append to `https://go.postman.co/environments/<env ID here>`. e.g. `https://go.postman.co/environments/10019550-b3c438b5-6bb0-4e90-8787-b936a0df00fe`. From here, the environment can be deleted altogether or the residing workspace can be identified through the top left workspace drop down, therefore allowing discovery and modification within Postman itself.


### The following request details can be ignored are internal to the scanners functionality.