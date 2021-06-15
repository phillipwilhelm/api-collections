This document explains how classified ads can be retrieved from Argus
Group car management software such as Planet VO, Planet VO 2 or Cardiff.
This is a REST API that returns JSON data. The document contains examples of requests using
the command line utility "curl" but requests can of course be made by any HTTP client.
This API is secured with OAuth 2.0 (https://oauth.net/), the industry-standard protocol for
authorization. Authentication is the required for every request. The authentication process is
described below.
Base URLs in this document are sample URLs (e.g. http://localhost:8080) definitive URLs for test
and production environmments along with credentials will be sent to you in due time.