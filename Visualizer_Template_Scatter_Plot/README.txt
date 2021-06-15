A collection of API requests to demonstrate the data visualization feature through a scatter plot, created by student developers at Berkeley CodeBase.

For the full list of visualizer templates we have created, click [here](https://explore.postman.com/templates/4424).

<br>

![alt text](https://raw.githubusercontent.com/isabelleyzhou/postman_visualizer_templates/master/scatter-plot/WorldTradingData.PNG "[Scatter Plot]")

<br>

This collection contains three sample templates for the scatter plot visualizer using requests from different API endpoints:

1. SchoolDigger
2. World Trading Data 
3. UFO 

For detailed explanation on a request, check its description.
<br>
<br>
**Visualization Data Parsing**
<br>
Data should be passed in as an array of datasets, where each dataset is a list containing points in the form [x,y]

Example:
```
[ 
	[ [x,y],[x,y],[x,y] ],
	[ [x,y],[x,y],[x,y],[x,y],[x,y] ]
]
```