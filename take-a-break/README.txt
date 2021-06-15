Given a date range, this is a postman collection allows you to find the best possible dates for a break so that a minimum number of leaves are taken. It is accessible directly from slack via `/take-a-break` command.

## Environment Variables
`airtable_api_key`, `goibibo_app_id`, `goibibo_app_key`, `postman_api_key`, `slack_webhook`

## Command Parameters
 - `from_date`: starting date 
 - `to_date`: ending date
 - `num_of_days`: number of days in the break
 - `src`: source airport IATA code(for searching flights)
 - `dest`: destination airport IATA code(for searching flights)