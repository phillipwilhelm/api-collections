A collection of API requests to demonstrate the data visualization feature through a cross filter, created by student developers at Berkeley CodeBase.

For the full list of visualizer templates we have created, click [here](https://explore.postman.com/templates/4424).

<br>

This tree allows us to visualize the JSON tree structure of any API response, including nested elements. Nodes of nested elements are fully collapsible and can be helpful for analyzing complex, heavily nested datasets.

<br>

![alt text](https://raw.githubusercontent.com/isabelleyzhou/postman_visualizer_templates/master/tree/NYT.png "[Tree]")

<br>

This collection contains three sample usages for the tree visualizer which visualizes the structure of an API response.

1. New York Times: Most Viewed Articles
2. Spotify: Top Tracks
3. Twitter: Top Tweets by Wendy's

For detailed explanation on a request, check its description.
<br>
<br>
**Visualization Data Parsing**

At the bottom of the test script, in the `parseData()` function, the data is formatted into the `dataTree` (structure shown below) by feeding in the data into the function `restructure(input, arr)`. 
<br>
<br>
```
var treeData = [
	"name": "root"
	"children": [
		{
			"name": "child1",
			"children": [
				{
					"name": "grandchild1"
				},
				{
					"name": "grandchild2"
				}
			]
		},
		{
			"name": "child2"
		}
	]
]
```

<br>
<br>

The only line of code that the developer needs to modify exists at the bottom of the test script. The input is one object in the API response. We are assuming that the API response is a list of repeated objects.
<br>
<br>
```
results: JSON.stringify(parseData(input))
```