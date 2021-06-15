A collection of API requests to demonstrate the data visualization feature through a bar chart, created by student developers at Berkeley CodeBase.

For the full list of visualizer templates we have created, click [here](https://explore.postman.com/templates/4424).

<br>

![alt text](https://raw.githubusercontent.com/isabelleyzhou/postman_visualizer_templates/master/bar-chart/OpenBrewery.PNG "[Bar Chart]")

<br>

This collection contains three sample usages for the bar chart visualizer.

1. Open Brewery DB
2. Yelp
3. School Digger

<br>

For detailed explanation on a request, check its description.
<br>
<br>
**Data Parsing**

At the bottom of the test script, the data is formatted into the following data structure, with `key` being elements of the x-axis and `frequency` being the value being plotted on the y-axis.

`
[{
	key: 'city-name',
	frequency: 34
}]
`