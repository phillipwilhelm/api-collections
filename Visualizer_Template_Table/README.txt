A collection of API requests to demonstrate the data visualization feature through a table, created by student developers at Berkeley CodeBase.

For the full list of visualizer templates we have created, click [here](https://explore.postman.com/templates/4424).

<br/>

![alt text](https://raw.githubusercontent.com/isabelleyzhou/postman_visualizer_templates/master/table/table_nyt.png "[Table]")

<br/>

This collection contains three sample usages for the table visualizer using requests from different API endpoints.

1. Pokemon 
2. Spotify 
3. New York Times

For detailed explanation on a request, check its description.
<br/>
<br/>
**Data Parsing**

Two arrays are feed into the template:

1. `headers` : an array of the table headers (strings)
	
	Example: `["header1", "header2", ...]`
	
	<br/>

2. `results` : an array of arrays, where each array contains a row of information

	Example: `[[name1, url1, summary1], [name2, url2, summary2], ...]`
	
	<br/>