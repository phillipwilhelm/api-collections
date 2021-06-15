Welcome to the appbase.io REST API Reference! appbase.io is a search service built on top of Elasticsearch, an Apache 2.0 licensed search engine. You can use it to build reactive apps, realtime maps, blazing fast search and recommendations, chats, feeds, IoT apps.

![appbase.io in one image](https://i.imgur.com/aaxqnN2.png)

You can read the intro guide to learn more about appbase.io over [here](https://docs.appbase.io/docs/gettingstarted/QuickStart/).

The below API is meant for the [apps product](https://appbase.io/apps) as it is a subset of the ElasticSearch API - specifically, the cluster management endpoints are inaccessible here. If you are using clusters, you can directly refer to the REST API for your ElasticSearch version [over here](https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html).

# Authentication

To authorize, use the `-u` flag with each request.

```bash
curl "api_endpoint_here" -u $credentials
```


Alternatively, you can set the `Authorization` header flag directly with "Basic + base_64($credentials)".

```bash
curl "api_endpoint_here" -h "Authorization: Basic YjdqV2hVSjhYOjcyYmI2ZmMxLWRkZjItNDU5Zi1iNGM3LWU2NzgwNjQyM2MyZA=="
```

All appbase.io endpoints require `$credentials`. appbase.io service offers two primary types of credentials:  


1. Read Only: These are good for apps that are published on the web where the credentials are visible, 
2. Read and Write: These are good for secure environments, servers and API users.

[Get your own credentials from your appbase.io dashboard.](https://dashboard.appbase.io)

# Metadata

Often times, there is a use for attaching a metadata with a request. appbase.io service supports adding metadata via the `X-Opaque-Id` header. This header when present in a request is spit back in the ElasticSearch response.

```bash
curl "api_endpoint_here" -H X-Opaque-Id:abracadabra
```

will return `X-Opaque-Id:abracadabra` back in the response header.