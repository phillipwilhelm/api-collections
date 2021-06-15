Get latest air quality metrics from [data.gov.in](https://data.gov.in) by city.

## Requirements

- Get an [API Key from data.gov.in][_api_key_url].
- Set the following [environment variables][_env]:
    - `api-key`: The API key you got from data.gov.in
    - `state`: The name of a state in India, in title case, e.g., `West Bengal`.
    - `city`: A city within that state, e.g., `Kolkata`.
- Optional environment variables:
    - `airtableURL`: An API URL for an Airtable Base where the max values of each pollutant is pushed.
    - `airtableKey`: The API Key for your Airtable account.

## Result

At the end of each run, a JSON array is saved in the environment variable called **`results`**. This variable value can be used in subsequent requests to push the data to some endpoint.

The structure of the JSON object is in the following format:

```
[
	"station": String,
	"<Pollutant ID>": {
		"min": Number,
		"max": Number,
		"avg": Number
	}
]
```

Each city can have multiple stations from where the pollution is monitored. There can be multiple pollutant information, depending on the stations. These include: `PM2.5`, `PM10`, `NO2`, `OZONE`, `CO`, `SO2` and `NH3`.

## Push to Airtable

You can configure this collection to push data to an Airtable. [Here is an example][_airtable_example] of such a table in action.

To do that, set up an Airtable with the following columns:

- `Station`
- `PM2.5`
- `PM10`
- `NO2`
- `OZONE`
- `CO`
- `SO2`
- `NH3`
- You can optionally add a column of type `"Created time"` to keep track of when the rows were inserted.

Once that is done, get the API endpoint for that table and add that in the `airtableURL` environment variable. You will also need your Airtable API Key, which needs to be put in the `airtableKey` environment variable.

To keep things single, this collection pushes only the `max` values of each pollutant. Feel free to hack on the structure in the "Pre-request script" of the "Post to Airtable" request.

[_env]: https://learning.getpostman.com/docs/postman/environments_and_globals/manage_environments/
[_api_key_url]: https://data.gov.in/help/how-use-datasets-apis
[_airtable_example]: https://airtable.com/shrivjWVlMZUNWB9M