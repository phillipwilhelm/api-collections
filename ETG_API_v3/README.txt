<img src="https://i.ibb.co/cFhW0FM/logos.png">
</br></br>
This documentation contains a general overview of the Emerging Travel Group API Partner Program.</br></br>
To know more about the benefits of our API integration or to sign up please check our <a href="https://www.ratehawk.com/lp/en/API">website</a>.</br></br>
Prior to starting to use the API, the respective agreement should be signed. After integration is completed, certification may be required.
<h1>Authorization</h1>
Emerging Travel Group API uses two API key sets granting you different kinds of access: <code>test</code> (<code>sandbox</code>) access and <code>production</code> access. <code>Test</code> API keys can only be used to book test hotels (<code>test_hotel</code>, <code>test_hotel_do_not_book</code>), while <code>production</code> API keys let you book all the hotels available via the <code>Emerging Travel Group</code> API (currently, this is the only difference between these 2 types of API keys).</br></br>

API key looks like <code>key_id:key</code>, where:
<table>
<tbody>
<tr>
<td><b>key_id</b></td><td>API key id</td>
</tr>
<tr>
<td><b>key</b></td><td>API key token</td>
</tr>
</tbody>
</table>

You may have several <code>production</code> keys across different contracts, e.g. to book properties across different markets.
<br/><br/>
The API keys that were created for your contract can be found in the <code>API</code> section of your contract's settings. 
<br/><br/>
For access to the relevant section, a <code>Master</code> account type is required.
<br/><br/>
The required authorization method is HTTP Basic Authentication (Basic Auth).
<br/><br/>
It is essential to bear in mind that every API-key endpoint has a limit to the number of requests. To discuss changes to this limit, please contact your account-manager. 
<br/><br/>
The limit to the number of requests per specified time period and number of remaining requests per current period and the timestamp of the limitation period's expiration are specified in the response:

    "X-RateLimit-SecondsNumber": 1 # amount of seconds, within which a number of requests not exceeding "X-RateLimit-RequestsNumber" can be executed
    "X-RateLimit-RequestsNumber": 10 # maximum amount of requests that can be executed within "X-RateLimit-SecondsNumber" seconds
    "X-RateLimit-Remaining": 9 # the remaining amount of requests (out of "X-RateLimit-RequestsNumber") in the current period of "X-RateLimit-SecondsNumber" seconds count
    "X-RateLimit-Reset": "2018-08-14T08:54:11" # DateTime (UTC+0) of expiration for period of "X-RateLimit-SecondsNumber" seconds' count.

<h1>Partner Contract Type</h1> 

<code>Emerging Travel Group</code> Partner Program offers two contract types:

<table>
<tbody>
<tr>
<td><b>affiliate</b></td><td><a href="https://docs.emergingtravel.com/#0542386d-febe-4883-af0e-3a068dadb4cf">Affiliate API</a></td>
</tr>
<tr>
<td><b>b2b</b></td><td><a href="https://docs.emergingtravel.com/#a88f5d7d-1a76-4784-845a-bf5fc077f176">B2B API</a></td>
</tr>
</tbody>
</table>

For more details on both types, please contact your Emerging Travel Group account-manager. Note that you can use one API key type for only one type of API partner contract. 

<h2>Important:</h2>

>Make sure that an <code>email</code> address for API-related questions is saved in the contract properties (contact type - <code>Technical questions and API</code>) - all notifications related to API and API-support will be forwarded only to this email address. Respective changes can be made in the <i>Contacts</i> section of your contract settings.

<h1>Request methods & format</h1>

Requests are made through <code>HTTPS</code> protocol via <code>GET</code> or <code>POST</code> methods.
Request data are always passed in <code>json</code> format in the request body (when using <code>POST</code>) or in GET-parameter <code>data</code> (when using <code>GET</code>).

<code>GET</code> example:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined">curl -g --user 'key_id:key' 'https://api.worldota.net/api/b2b/v3/hotel/info/?data={"id":"city_hotel_berlin_east","language":"en"}'
</code></pre>
</br>
<code>POST</code> example:
</p>
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined">curl --user 'key_id:key' --data '{"id":"city_hotel_berlin_east","language":"en"}' "https://api.worldota.net/api/b2b/v3/hotel/info/"
</code></pre>

<h1>Response Format</h1>

Response format is always <code>json</code>.

Top-level response keys

<table>
<tbody>
<tr>
<td><strong>data</strong></td><td>Main content of the response.</td>
</tr>
<tr>
<td><strong>debug</strong></td><td>Additional content to the response, containing initial requests parameters in <code>json</code> format and/or <code>http status code</code> value.</td>
</tr>
<td><strong>error</strong></td><td>Fields with <a href="https://docs.emergingtravel.com/#errors">error description</a>, shown if error occurs.</td>
</tr>
<tr>
<td><strong>status</strong></td><td>Response status code.</td>
</tr>
</tbody>
</table>

<p>For example:</p>

<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": {
        "data_3ds": null,
        "partner_order_id": "asd123",
        "percent": 100
    },
    "debug": null,
    "error": null,
    "status": "ok"
}
</code></pre>

<h1>Errors</h1>

<h2>Syntax error</h2>
JSON has syntax rules that describe how the data must be stored. If the data gets corrupted and no longer complies with the rules, an error occurs:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "api_endpoint": {
            "endpoint": "api/b2b/v3/hotel/info/",
            "is_active": true,
            "is_limited": true,
            "remaining": 9,
            "requests_number": 10,
            "reset": "2018-08-16T12:12:37",
            "seconds_number": 1
        },
        "api_key_id": 1304,
        "method": "GET",
        "real_ip": "62.76.100.3",
        "request_id": "68c1141361db8c82835ea268486d7c6f",
        "utcnow": "2018-08-16T12:12:36.328390"
    },
    "error": "decoding_json",
    "status": "error"
}
</code></pre>

<h2>"Exceed limit" error</h2>
If you have exceeded the requests number limit for your endpoint, the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "api_endpoint": {
            "endpoint": "api/b2b/v3/hotel/info/",
            "is_active": true,
            "is_limited": true,
            "remaining": -1,
            "requests_number": 1,
            "reset": "2018-08-16T12:32:40",
            "seconds_number": 20
        },
        "api_key_id": 496,
        "method": "GET",
        "real_ip": "10.11.0.23",
        "request_id": "8dd3efd24bdd6a9272770936e5108f8c",
        "utcnow": "2018-08-16T12:32:26.161565"
    },
    "error": "endpoint_exceeded_limit",
    "status": "error"
}
</code></pre>
To discuss the changes to this limit please contact your account manager.

<h2>"Is active" error</h2>
If your endpoint was deactivated, the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "api_endpoint": {
            "endpoint": "api/b2b/v3/hotel/info/",
            "is_active": false,
            "is_limited": true,
            "requests_number": 1,
            "seconds_number": 20
        },
        "api_key_id": 496,
        "method": "GET",
        "real_ip": "10.11.0.23",
        "request_id": "61c015d15d325f0bb945db5d027fc35c",
        "utcnow": "2018-08-16T12:38:38.481018"
    },
    "error": "endpoint_not_active",
    "status": "error"
}
</code></pre>
To discuss the changes to this activation please contact your account manager.

<h2>"Endpoint not found" error</h2>
If you do not have permission to use this method, the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "api_key_id": 1775,
        "method": "POST",
        "real_ip": "10.11.0.23",
        "request_id": "45141c733a1f4d534a0518c513d3641b",
        "status": 403,
        "utcnow": "2018-08-14T12:51:58.715639"
    },
    "error": "endpoint_not_found",
    "status": "error"
}
</code></pre>
To discuss the changes to this please contact your account manager.

<h2>Error in case of using incorrect API credentials / having no permission to use the API</h2>
If you used incorrect API credentials (or if you don't have permission to use the API), the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "real_ip": "52.29.104.100",
        "request_id": "e6ff36a9e635825743e7ded8c05739a0",
        "utcnow": "2018-08-23T09:34:43.673713"
    },
    "error": "incorrect_credentials",
    "status": "error"
}
</code></pre>
Please note that in case of recurring unauthorized requests over a considerable period of time, we may ban the IP-address from which such requests are sent.

<h2>"Auth header" error</h2>
If you do not use the correct authorization:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "real_ip": "52.29.104.100",
        "request_id": "563c919d77000963a4ef9ade0988b21b",
        "utcnow": "2018-08-23T10:03:28.794712"
    },
    "error": "no_auth_header", #or "invalid_auth_header"
    "status": "error"
}
</code></pre>
Check the <a href="https://docs.emergingtravel.com/#authorization">Authorization section</a> of the documentation.

<h2>"Invalid params" error</h2>
If you do not input all the required data:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "api_endpoint": {
            "endpoint": "api/b2b/v3/hotel/order/info/",
            "is_active": true,
            "is_limited": true,
            "remaining": 9,
            "requests_number": 10,
            "reset": "2018-08-23T09:59:38",
            "seconds_number": 1
        },
        "api_key_id": 1304,
        "method": "POST",
        "real_ip": "52.29.104.100",
        "request_id": "7f4937bdabe8bb13d4980dcd77a16117",
        "utcnow": "2018-08-23T09:59:37.495757",
        "validation_error": "value \"page_number\" is required but None"
    },
    "error": "invalid_params",
    "status": "error"
}
</code></pre>
Check the <code>validation_error</code> and add the required data.

<h2>"Lock" error</h2>
In case you try to make the same request with the same <code>partner_order_id</code> more than once at the same time, the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "real_ip": "52.29.104.100",
        "request_id": "2c2264a2f3f64b9032624e99ddd49976",
        "utcnow": "2018-08-23T11:43:27.101799"
    },
    "error": "lock",
    "status": "error"
}
</code></pre>

<h2>"Not allowed host" error</h2>
If it is forbidden to make a request from your host, the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "real_ip": "52.29.104.100",
        "request_id": "7b76e52a742f714e6686761fab48cfa3,
        "utcnow": "2018-08-23T11:31:44.235203"
    },
    "error": "not_allowed_host",
    "status": "error"
}
</code></pre>
Please contact the API support team.

<h2>"Not allowed" error</h2>
If it is forbidden to make a request with this endpoint, the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "real_ip": "52.29.104.100",
        "request_id": "7b76e52a742f714e6686761fab48cfa3,
        "utcnow": "2018-08-23T11:31:44.235203"
    },
    "error": "not_allowed",
    "status": "error"
}
</code></pre>
Please contact your account manager.

<h2>"Overdue debt" error</h2>
If you have an overdue debt, the following error will be returned:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "real_ip": "52.29.104.100",
        "request_id": "36f4a2ae479cc0eba8e3ddf7d09bba14",
        "utcnow": "2018-08-23T10:11:08.045023"
    },
    "error": "overdue_debt",
    "status": "error"
}
</code></pre>
Please contact your account manager.

<h2>"Unexpected method" error</h2>
If you make a request with an unsupported GET/POST method:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": {
        "api_key_id": 1304,
        "real_ip": "52.29.104.100",
        "request_id": "19925f65c2763212bbe37294178b6fa6",
        "utcnow": "2018-08-23T09:56:37.677774"
    },
    "error": "unexpected_method",
    "status": "error"
}
</code></pre>
Use POST/GET instead.

<h2>Unknown error (example)</h2>
When something has gone wrong:
<pre class="click-to-expand-wrapper is-snippet-wrapper is-expandable language-undefined"><code class="is-highlighted language-undefined"> {
    "data": null,
    "debug": null,
    "error": "unknown",
    "status": "error"
}
</code></pre>
Errors with status 500 may be returned, for example, because of an internal <code>Emerging Travel Group</code> services' timeout. A request shall be sent again (the number of recurrent identical requests must be limited).

<h1>Integration Guideline</h1> 

***Recommended workflow:***
1. <a href="https://docs.emergingtravel.com/#0b55c99a-7ef0-4a18-bbfe-fd1bdf35d08e">Hotel Static</a> (should be used for downloading content and mapping hotels)
2. <a href="https://docs.emergingtravel.com/#09dada83-ed9e-400e-a793-517d078e9df9">Search Engine Results Page</a> (should be used for available hotels searches)
3. <a href="https://docs.emergingtravel.com/#67876b90-43ba-40e9-883b-a63a69b1be79">Hotelpage</a> (should be used only for hotels that your end-user wants to know about; that is, you should not initiate HP search automatically for all hotels, returned by a region search)
4. <a href="https://docs.emergingtravel.com/#18ad54c3-07dc-4515-9c02-4ff391ac6085">Order Booking Form</a> + <a href="https://docs.emergingtravel.com/#b79e9280-16da-4d51-b500-7f1c3bfd0f78">Order Booking Finish</a> (should be used for creating a new booking)
5. <a href="https://docs.emergingtravel.com/#09e1f183-0fef-49af-8c76-c8a8fa3d9036">Order Booking Finish Status</a> or <a href="https://docs.emergingtravel.com/#b2a21496-9c3b-46d9-b9db-f8d44881b125">Order Status Webhook</a> (should be used for receiving final booking status)
6. <a href="https://docs.emergingtravel.com/#ce9ab2ee-fec0-4850-9435-a894fd09ca0c">Order Information</a> (should be used for receiving information on a completed booking)
7. <a href="https://docs.emergingtravel.com/#42df67f8-653f-4356-ac1e-01526501bd94">Order Cancellation</a> (should be used for a booking cancellation, if needed)

*It is important to note that if the Emerging Travel Group system returns one of 5xx errors, this does not mean that the request was unsuccessful. Errors with status 500 may be returned, for example, because of internal Emerging Travel Group services' timeout. The request should be sent again (the number of recurrent identical requests must be limited).*

***Recommendations for usage of static data:***
- It is recommended to update the static data every day via Hotel Incremental Data Dump. Otherwise the static data should be updated at least once a week via Hotel Data Dump. 
- It is obligatory to show hotels "important information" ("metapolicy_extra_info" and "metapolicy_struct" params in the dump file), as these params include hotel rules and information on a chargeable services. 

***Search flow recommendations:***

Generally, while using the first search step (Search Engine Results Pages) we recommend showing one or two of the cheapest rates for each hotel and on the second search step showing all the rates for one specific hotel. 

We do not recommend using rates matching because:
- not all of the suppliers allow you to make a booking from the first search step
- not all of the suppliers provide all the necessary response data (e.g. cancellation policies) at the first search step
- not all of the suppliers provide all available rates for the hotel at the first search step (e.g. there are suppliers that respond only with one rate, the "cheapest", so you will miss other rates)
- the first search step is slower so not all of the rates will be returned if you have a short search timeout
- the first search step has a longer cache life

The point is that when using rates matching flow you are missing lots of the rates and have a higher fail-ratio at the valuation step.

If you still intend to match the rates between the <a href="https://docs.emergingtravel.com/#09dada83-ed9e-400e-a793-517d078e9df9">Search Engine Results Page</a> and <a href="https://docs.emergingtravel.com/#67876b90-43ba-40e9-883b-a63a69b1be79">Hotelpage</a> steps please use the <code>match_hash</code> param from the search response.
  
*Other important points of the search flow:*

*It is obligatory to showing taxes, which Emerging Travel Group provides in the rate details.*

*The full room type (“room_name”) received in the rates details should be shown on your side.*

***Booking flow recommendations:***
To obtain the final status of the booking you can use the <a href="https://docs.emergingtravel.com/#09e1f183-0fef-49af-8c76-c8a8fa3d9036">Order Booking Finish Status</a> or <a href="https://docs.emergingtravel.com/#b2a21496-9c3b-46d9-b9db-f8d44881b125">Order Status Webhook</a>. If you use the Order Booking Finish Status we recommend that you check the status of the booking every 5 seconds until the final status is obtained. If you have any limitations for this step, please discuss it with our API support team. 


***Please note that this Guide does not include all the possible API usage rules. Every endpoint has a detailed description and a description of available params. If you have any questions related to API usage, please send it to the API support team.***

After the integration is completed you need to proceed with the certification and provide access to your test/dev website where our API is implemented.


<h1>API Support request recommendations</h1>
<div id="common-recommendations" class="section">
<h2>Common recommendations</h2>
<ul class="simple">
<li>Specify the issue as clearly as possible.</li>
<li>Always highlight the goal you want to achieve.</li>
<li>Please note, that existing functionality of the API is always described in the documentation.</li>
</ul>
</div>
<div id="reporting-details-of-the-issues-or-inquiries" class="section">
<h2>Reporting details of the issues (or inquiries)</h2>
<ul class="simple">
<li>Always mention the exact method (with its endpoint in URL).</li>
<li>Provide an example of a request that causes the issue (in the format in which it was sent to us).</li>
<li>If you provide response logs, please specify them in JSON format (the only format, that is currently supported).</li>
<li>Specify the issue's timestamp - this can also help to determine the issue's cause.</li>
</ul>
</div>
<div id="identification" class="section">
<h2>Identification</h2>
<ul class="simple">
<li>Specify your contract's number for easier identification.</li>
<li>Specify the key_id of the API key you were using.</li>
</ul>
</div>
<div id="addressees-of-the-request" class="section">
<h2>Addressees of the request</h2>
<ul class="simple">
<li>If the question regarding the API is forwarded to na on-tech support manager, its processing can take a longer time - as you may be forwarded to an API tech support manager.</li>
<li>In case an inquiry which is not related to API is forwarded to API tech support manager, it's processing can take a longer time as well, as you may be forwarded to your account manager (or, if applicable, to another responsible manager).</li>
</ul>
</div>