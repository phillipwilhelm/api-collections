This is a ready made Line Graph using ChartJS to help you get started quickly with [data visualization in Postman](https://learning.getpostman.com/docs/postman/sending_api_requests/visualizer/). 

The data here is from https://worldtradingdata.com. Sign up for a free 250 daily requests to get access to a plethora of stock data, current and historical! 

You will see an object called `vizData` in the "Tests tab". You will have edit bind the data from the response you get to the `vizData` variable. It has four properties:

- `symbol`: This takes a stock symbol string
- `stockX`: This take an string stock exchange
- `labels`: This takes an array of "date" strings that will serve as labels on the data items
- `data`: This takes an array of numbers that form the first dataseries of the chart