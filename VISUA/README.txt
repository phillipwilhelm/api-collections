Welcome to the VISUA API documentation. Here you will find technical resources and examples for building _Visual-AI_ applications using VISUA. Popular _Visual-AI_ use cases include:
* **Media Monitoring and Intelligence**: to evaluate ROI of marketing campaigns, compare share of voice and measure consumer sentiment.
* **Market Research**: to extract consumer insights by correlating different visual signals across a variety of media.
* **Brand Protection**: to detect counterfeit products, identify illegal use of copyrighted material and support compliance in online marketplaces.
* **Sports Sponsorship**: to accurately measure the amount and quality of sponsors' exposure during sporting events and related content (user-generated or licensed).
* **Ad Tech**: to track advertising activity across multiple channels, automate creative testing and Ad verification.
* **Content Moderation**: to flag inappropriate content, extremist material and dangerous brand associations.

Depending on your use case you might use a combination of the following technologies, generally available to all developers:
* [Logo & Mark Detection](https://docs.visua.com/?version=latest#fca618fa-3dae-4ad5-b48b-487362186626)
* [Visual Search](https://docs.visua.com/?version=latest#bc2425e2-db84-41b7-a3d3-fd9785c411cd)
* [Text Detection](https://docs.visua.com/?version=latest#ac5e5aef-30c3-42ef-aa35-52c4302e1b16)
* [Object & Scene Detection](https://docs.visua.com/?version=latest#6776c6c3-5359-4df7-8a0d-bb3fa0285ec4)
* [Ad Detection](https://docs.visua.com/?version=latest#087152c3-1a53-4968-9d9b-df01efb575cc)

If you have any questions you can contact our team at <support@visua.com>.

# Authentication and Security

When signing up to VISUA you will receive a personal developer key (referred as `YOURKEY`) which is used to authenticate the requests you will be making to the VISUA API.

The preferred way is to include your developer key in the header of your requests. This method of authentication is used in all the examples shown below. Nonetheless we accept it also as query parameter or in the request body. The following table summarizes the different ways to authenticate your requests:

| Method | Implementation |
| --- | --- |
| header                | `-H "X-DEVELOPER-KEY: YOURKEY"` |
| x-www-form-urlencoded | `-data developerKey=YOURKEY` |
| form-data             | `-form developerKey=YOURKEY` |
| query param           | `-url 'https://api.visua.com/detect?developerKey=YOURKEY'` |

Even though the _HTTP_ protocol is supported, we strongly recommend to use _HTTPS_ so that header, body and response will all be encrypted.

All API endpoints are secure _HTTPS_ endpoints with _SSL/TLS_ to ensure secure client-server communications. The client-server communication is encrypted and authenticated using a strong protocol (_TLS 1.2_), a strong key exchange (_ECDHE-RSA_ with _P-256_) and a strong cipher (_AES-128-GCM_).

# Rate Limiting

Each API endpoint observes rate limits that define the maximum number of requests that can be made over a specific time window.

The [Limits endpoint](https://docs.visua.com/?version=latest#1624adb2-a683-49b9-8030-41eee296e1ff) returns what the maximum number and the time window is for each endpoint.

To facilitate managing your rate limit, each API response includes HTTP Headers detailing your current usage level. The following table illustrates the different HTTP Headers returned with every response:

| Name | Description |
| --- | --- |
| `X-RateLimit-Limit` | Request limit per time window |
| `X-RateLimit-Time` | Time window length in seconds |
| `X-RateLimit-Remaining` | Number of requests left for the current time window |
| `X-RateLimit-Reset` | Start Timestamp (unix epoch) for the next time window |

Requests exceeding the given rate limit will respond with status code `429 Too Many Requests`.

In the case of [On-demand detection](https://docs.visua.com/#3dfadb11-a78d-411e-9309-fce55b3c96e6) there is no rate limit for the number of media submitted. The API response instead includes HTTP Headers detailing useful information to help you manage your submissions:

| Name | Description |
| --- | --- |
| `X-OnDemand-SubmissionRate` | Number of media submitted in the last minute |
| `X-OnDemand-Throughput` | Number of media processed in the last minute |
| `X-OnDemand-Outstanding` | Number of media waiting to be processed |
| `X-OnDemand-Delay` | The age in seconds of the oldest Outstanding media |

When `Throughput` is higher than or equal to `SubmissionRate`, the number of `Oustanding` is zero and so is `Delay` since the resources currently provisioned are enough to process your submissions as they come in. During sustained periods where `SubmissionRate` is higher than `Throughput`, the `Oustanding` media will temporarily increase while more resources are provisioned. During these periods the `Delay` will also increase as it relates to the age of the oldest media waiting to be processed. The _On-demand_ headers are updated every minute.

# Dry Run 

_Dry Run_ mode can be used to issue dummy requests against the VISUA API in order to validate your code, for example as part of your [Unit](https://en.wikipedia.org/wiki/Unit_testing) or [Integration](https://en.wikipedia.org/wiki/Integration_testing) testing.

In _Dry Run_ mode the endpoint execution will not alter the state of your VISUA account. This means that no data will be persisted or updated and the request will not be counted against your quota.

A _Dry Run_ request can be issued by adding an additional header parameter called `dryRun` with value `true`. Not all endpoints support this mode and the API will respond with status code `501 Not Implemented` if a specific endpoint does not implement _Dry Run_ mode.

Endpoints implementing _Dry Run_ offer more details on its behaviour in the dedicated _Dry Run_ section of the endpoint description.

# Encoding

In all the following examples you will notice the header parameter:

`Content-Type: application/x-www-form-urlencoded`

This means that we require you to [encode](https://en.wikipedia.org/wiki/Percent-encoding) the value of each parameter you pass to any endpoint.

Special attention should be given when encoding parameters that contain a `+` (plus) character. Because `+` [has been treated also as a shorthand for space](https://www.w3.org/Addressing/URL/4_URI_Recommentations.html) its decoding is ambiguous. You should first replace `+` with its corresponding encoding `%2B` and then encode the whole parameter. For example if your parameter is `x+y/z`, the plus sign should be encoded separetely resulting in `x%2By/z` and finally the parameter should be encoded as `x%252By%2Fz`.