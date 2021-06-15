This collection recommends which Caches Clusters in AWS ElastiCache are inactive in a given range of time with few externally specified constraints. It uses CloudWatch to get the statistics of clusters and currently is based on 3 metrics: 

* CacheHits
* CPUUtilization
* CurrItems

Setup
====================
You need to set the following environment variables:

1. AWS Credentials 

    a. `accessKeyID`

    b. `secretAccessKey`

2. `slackWebHookURL` 

    *Description: Collection notifies its results on this webhook.*

3. `region`

    *Description: AWS region to monitor - Ex: 'us-east-1'*

4. `days`

    *Description: Range to monitor clusters starting from today to back N days*

5. `period`

    *Description: Time interval in which AWS collects data points and aggregates them. Ex: 36000 (seconds)*

Miscellaneous
====================
1. AWS allows **1440 data points** in a single request. Either make period long or days short so that data points aggregated are less than their limit. 

2. Parameters below have **default values** in case not mentioned in the environment. You can modify these in the environment if required. However, these are recommended.



<table>
	<tr>
		<th>Variable Name</th>
		<th>Default Value</th>
	</tr>
	<tr>
		<td>days</td>
		<td>14</td>
	</tr>
	<tr>
		<td>period</td>
		<td>36000</td>
	</tr>
	<tr>
		<td>region</td>
		<td>us-east-1</td>
	</tr>
</table>