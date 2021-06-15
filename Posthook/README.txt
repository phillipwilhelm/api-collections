The **Posthook** API lets developers schedule requests to be made back to their application at specified times in the future.

```shell
curl https://api.posthook.io/v1/hooks \
  -H 'X-API-Key: {{apiKey}}' \
  -H 'Content-Type: application/json' \
  -d '{
        "path": "/webhooks/ph/event_reminder",
        "postAt": "2018-05-03T01:11:55Z",
        "data": {
          "eventID": 25
        }
      }'
```

This is the main API call your application will be making to schedule new **Hooks**. **Posthook** will then wait until the **postAt** time and attempt to call back to your application as explained in the "Hooks Fulfillment" section below.

Note that the domain is not specified when scheduling new **Hooks**. This is because we tie the domains to **Projects** in order to allow domains to be changed without having to change all your scheduled hooks for that project. Also note that we only support calling back to your application in **HTTPS** so your webhooks handling **Posthook** requests will need to served in **HTTPS**.


# Authentication

We use API Keys for Authentication. You can retrieve your API Key under your [Account Settings](https://posthook.io/app/account#projects). Provide your API Key as the value for the `X-API-Key` header.

All API requests must be made over [HTTPS](https://en.wikipedia.org/wiki/HTTPS) and include an API Key.

# Hook Fulfillment

Posthook will try to make a POST request to your application at the specified *postAt* time **at least once** for each **Hook**. Even though in most cases this request will only happen once per hook, it is possible that in certain failure scenarios it will happen more than once. If your use case requires an action to happen only once it is recommended you validate it still needs to happen by checking in a database, for example.

This request can be replicated with this example curl:

```shell
curl https://www.example.com/webhooks/ph/event_reminder \
-H `User-Agent: Posthook/1.0` \
-H `Content-Type: application/json` \
-H `X-Ph-Signature: 428354c940d6c634291f70537d202517466191f0b50c07bbe7f4307be11765ec` \
-d `{
		"id":"98ff3a11-7677-480b-9f40-8c1035e09381",
		"path":"/webhooks/ph/event_reminder",
		"postAt":"2018-05-03T01:11:55Z",
		"postedAt":"2018-05-03T01:11:55.0107686Z",
		"data":{
			"eventID":25
		},
		"createdAt":"2018-05-03T01:11:52.466482Z",
		"updatedAt":"2018-05-03T01:11:53.460343Z"
	}`
```

Posthook, by default will attempt to make this request twice, waiting for 5 seconds after the first attempt. This behavior can be modified under your [**Project**'s settings](https://posthook.io/app/account#projects). It will consider a failure any response with a status code that is not '200'. It will also timeout and consider a failure any request taking longer than 10 seconds, so it is important to do any long-running work asynchronously to avoid the request timing out and potentially retried. After Posthook has exhausted the number of retries configured for the project, it will notify you based on your [notification settings](https://posthook.io/app/account#notifications) and set the Hook's status to "failed". Your application would then able to recover from failed hooks by querying the `/v1/hooks` endpoint for failed hooks and catching up on the appropriate work.

## Security

**Calls back to your application are made over HTTPS only**. If you are developing locally we recommend using a service like [ngrok](https://ngrok.com/). These calls back also include a `X-Ph-Signature` header. Your application can optionally (though highly recommended, but depends on how you're using Posthook) verify that requests are coming from **Posthook** by verifying this signature. The signature is generated using a hash-based message authentication code ([HMAC](https://en.wikipedia.org/wiki/HMAC)) with [SHA-256](https://en.wikipedia.org/wiki/SHA-2). Compute the HMAC using the JSON payload (the request body) and your account's [signing key](https://posthook.io/app/account#signing_key) and compare it to the signature in the `X-Ph-Signature` header in the request.

# Sequences

Sequences let you configure Posthook to automatically create hooks given a start date/time, an interval, and a list of paths.

## Settings

### Name

A name to help you identify the Sequence.

### Start At

Date and time when the Sequence will first run at.

### Repeat Interval

The time interval between each run of the Sequence.

If *Start At* is set to `2018-01-01T01:15:00Z`, a repeat interval set to 1 hour will run the Sequence at every 15 minutes past the hour.

### Steps

A set of paths hooks will be created for and the dependencies between them (in YAML format).

Each step has two properties:

**path (required)**: the URL path for this step in the Sequence

**requires (optional)** : a list of steps that are required to run successfully before this step's hook will be created

In the example below, *getExchangeRates* and *getWeather* will both start running at the beginning of the Sequence. If they are both successful, *refreshCache* will run. And finally, *reportSuccess* will run if *refreshCache* is successful.

```shell
getExchangeRates:
  path: /ph/get_exchange_rates
getWeather:
  path: /ph/get_weather
refreshCache:
  path: /ph/refresh_cache
  requires:
    - getExchangeRates
    - getWeather
reportSuccess:
  path: /ph/report_success_slack
  requires:
    - refreshCache
```
