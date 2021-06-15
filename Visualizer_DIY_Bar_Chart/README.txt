This is a readymade Bar Chart using ChartJS to help you get started quickly with [data visualization in Postman](https://learning.getpostman.com/docs/postman/sending_api_requests/visualizer/). All you need to do is bind the right data in the right format to the template. Check the "Tests" tab in the request for details.

The data used in this example is generated using Postman's dynamic variables, along with the Postman Echo service. You can edit the request and change the URL any endpoint of your choice.

You will see an object called `vizData` in the "Tests tab". You will have edit bind the data from the response you get to the `vizData` variable. It has two properties:

- `labels`: This takes an array of strings that will serve as labels on the data items
- `data`: This takes an array of numbers that form the first dataseries of the chart