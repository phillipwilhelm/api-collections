# Common

The following paragraph describes a set of advanced operations that could be applied in the REST APIs.

We support the following features:
* Pagination
* Filtering
* Sorting

---

## Pagination in the REST API: 

### Why pagination?

A PTNetsuite REST API response potentially provides plenty of data. Under this condition, a feature to limit the incoming info and split it into chunk of data is a highly valuable tool. Precisely for this reason the pagination functionality is provided: using the pagination the API response info is much easier to handle.

### Set and understand the parameters
The paging functionality allows to split the server response, setting a limit and an offset to the number of items returned in the API response.

The following fields are present in all the `GET` method that return a `rows` object:
* `offset`: the index of the first item in the response
* `limit`: the maximum number of items in the response
* `size`: the total number of items in the response

If `limit` : 5 and `offset` : 0, the response returns at most the first five elements (from 0 to 4).

If `offset` : 5 and `limit` : 2, we return elements from 5 to 6.

#### How do we know if there are more pages?

The total number of pages depends on the provided `limit` and `size`.

For example, if `limit`:5 and `size`:10, the total number of pages will be 2.

#### Limitations

The maximum value for `limit` is 100, bigger values will be replaced by the max value. Hence, 100 elements will be returned at most.

---

## Filtering:

Filters are perfect if ou want that the response provides only a subset of the whole result of a `GET` REST API. The filter is set using the query string format: 

```
/api/v2/{resource}?{{key}}={{value}}
```

where:
   * `{resource}`
   * `{{key}}` available keywords are listed in the API page
   * `{{value}}`

It's possible to provide N pairs `{{key}}={{value}}` separated by `&` (see query string URL notation)

An example for the `gateway-profiles` resource is:

`/api/v2/gateway-profiles?band=EU863-870&maxTxPower=27`

it provides a filter to get the list of the gateway profiles with band=EU863-870 and maxTxPower=27.

Note that each REST API has its own filters.

## Sorting:

The `GET` REST APIs provide the logic to set the order of the items in the response. Sorting is set by the `sort` query string parameter:

```
/api/v2/{resource}?sort={{key1}}:{{method}},{{key2}}:{{method}}
```

Where the available `{{method}}` values are:

* `desc`: descending order
* `asc`: ascending order

and the `{{key}}` depends on the REST API that we want to use.

For example, let's use the method `GET` on the resource `gateway-profiles` setting the descending order on `createdAt` timestamp:

```
/api/v2/gateway-profiles?sort=createdAt:desc
```

For a sort in cascade:
```
/api/v2/gateway-profiles?sort=createdAt:desc,id:asc
```

## Filtering & Sorting:

To set a filter and sort the result we provide the possibility to concatenate both the functionalities:

For example, let's use the method `GET` on the resource `gateway-profiles` to get all the profiles with a `band=EU863-870` and `maxTxPower=14` setting the ascending order on `id`:

```
/api/v2/gateway-profiles?band=EU863-870&maxTxPower=14&sort=id:asc
```

---

## Response in the REST API: 

In the response,  there are also some informations:
* `createdAt`: indicate the timestamp set when we create the required item
* `updatedAt`: indicate the timestamp of the last item's update

---

# Error Code:

All the REST API may return one of the following error code as response: 

| Status | Description | Solution 
| --- | --- | --- | 
| 400 | Bad Request | The request could not be fulfilled due to syntax errors. The errors can be present both in the query string and in the body of the call.
| 401 | No authorization | Get an authorization token after login using credentials that can access the desired resource 
| 403 | Forbidden | The user cannot access the requested resource
| 404 | Not Found | The requested resource was not found

## Error code example: 

Return code 400:

```
{
    "status": 400,
    "message": "params should NOT have additional properties"
}
```

Return code 401: 
``` 
{	"status": 401, 
	"message": "No authorization token was found", 
	"code": "credentials_required", 
	"inner": { 
		"message": "No authorization token was found" 
	} 
} 
```

Return code 404:

```
{
    "status": 404,
    "message": "Gateway not found"
}
```

--- 

# Used tools

Documentation created with:

https://github.com/adobe/jsonschema2md