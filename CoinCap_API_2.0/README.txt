v2.0.1-beta

CoinCap is a useful tool for real-time pricing and market activity for over 1,000 cryptocurrencies. By collecting exchange data from thousands of markets, we are able to offer transparent and accurate data on asset price and availability. 

Our API will offer insight into exactly which exchanges and markets contribute to our pricing. 

For all endpoints, a single page offers 100 responses by default and supports up to 2,000 responses per page upon requests. 

## Status Codes and Error Response

The following are error codes you may encounter as you use CoinCap.
  Note: all CoinCap requests are GET requests

200: Successful - this is the data you were looking for

400-417: Client error - these will often be accompanied by some response in the body that will give the user direction on how to change the request. Here are some examples of 400: Bad Request responses:
- 'use valid interval': m1, m15, h1, d1': Interval must be m1 for one minute, m15 for 15 minute, h1 for one hour, and d1 for one day
- 'query requires end': If user includes a start query, there must be an end query
- 'query requires start': If user includes an end query, there must be a start query
- 'limit exceeds 2000': bad request, exceeds max limit
- 'missing exchange': This endpoint requires user to specify exchange in parameters
- 'missing interval': This endpoint requires user to specify interval (ex: m1, m15, d1, etc) in parameters
- 'missing base': This endpoint requires user to specify base asset (ex: BTC)
- 'missing quote': This endpoint requires user to specify quote asset (ex: USD)

500-505: Server Error - Looks like something went down on our end. Try back again soon!

For a full list of HTTP Status Code definitions, please visit [here](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).

## Headers

We encourage clients to use compression via the `Accept-Encoding` header.

`Accept-Encoding: gzip` or `Accept-Encoding: deflate`
