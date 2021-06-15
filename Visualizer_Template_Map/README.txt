A collection of API requests to demonstrate the data visualization feature through a density map, created by student developers at Berkeley CodeBase.

For the full list of visualizer templates we have created, click [here](https://explore.postman.com/templates/4424).

<br>

This global density map allows us to visualize any form of quantitative variable, such as population, temperature, or number of occurrences, against longitude and latitude coordinates.

<br>

![alt text](https://raw.githubusercontent.com/isabelleyzhou/postman_visualizer_templates/master/map/map_earthquakes.png "[Map]")

<br>

This collection contains three sample usages for the map visualizer.

1. Earthquakes
2. Unemployment Rate
3. UFO Sightings

<br>

For detailed explanation on a request, check its description. 

<br>

**Data Parsing**

At the bottom of the test script, the data is formatted into the following data structure.

`[{ lat: 75.0, long: 36.0, circleSize: 8, color: '#FFFFFF' }]`

<br>

**Custom Tooltip** 

The default tooltip description is the latitude and longitude of the point. If you wish to edit the tooltip description, add the desired fields to `parsedData` and edit the tooltip section of the template. See the "Unemployment Rate" example for reference.

<br>

**Map Use**

Drag to select an area to zoom into, single click to zoom out, and hover to view ToolTip tags.