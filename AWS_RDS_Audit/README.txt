A simple collection to monitor RDS Instances. Auditing environments involves the following steps:

1. Fetch all instances using the provided access key id and secret token.
2. If there are additional instances to be fetched beyond the response of the first fetch request, extract the pagination token from the response and use it to repeat the fetch request.
3. Once there are no more instances to be fetched, save the list of instances as an environment variable.
4. Iterate over the list, repeating the configuration description request for each instance in the list. Once the config for an instance is known, compare it to a set of expected results to ensure compliance.

PS: This collection is most useful when run as a [monitor](https://www.getpostman.com/docs/postman/monitors/monitoring_apis_websites), so as to run such audits on a periodic basis. You can also configure the inbuilt Slack integration for Postman monitors, so as to recieve instance alerts when things are amiss.

# Required environment variables:
This collection requires the following environment variables:

|    Name    |                         Description                                          | Required |
|:----------:|:----------------------------------------------------------------------------:|:--------:|
|     id     |          The access key id for the audit AWS user                            |    Yes   |
|    key     |        The secret access key for the audit AWS user                          |    Yes   |
| awsRegion  | The region to audit environments in. Defaults to us-east-1                   |    No    |
| maxRecords | The number of environments to retrieve per fetch call. Defaults to 100 (max) |    No    |