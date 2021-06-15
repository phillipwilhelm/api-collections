This collection is an example of how to [use the Postman Collection Runner alongside CSV or JSON data files](https://www.getpostman.com/docs/v6/postman/collection_runs/starting_a_collection_run). Read more about it in [this blog post](https://blog.postman.com/looping-through-a-data-file-in-the-postman-collection-runner/).

We will run this collection using one of these data files, exported from Google Search Trends about [the volume of searches for "Ramen" by city](https://trends.google.com/trends/explore?q=Ramen). ????

If you don't have these data files, download these examples:
- [JSON file](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen.json)
- [CSV file](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen.csv)

### Get Started

To run a collection in the Postman app, click on the chevron (>) next to the collection's name to expand the details view. Select the blue **Run** button to open the Collection Runner in a new window.

![[collection details](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen-app.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen-app.png)

Verify the collection and environment (if any). Select "Choose files", and load the data file in the collection runner. If the data file was loaded successfully, you can preview the values within the Collection Runner.

![[data files preview](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen-preview.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen-preview.png)

The iteration count can be anything from 1 to 3. If the number of iterations specified is greater than the number of rows in the data file (excluding the column headers), then the collection runner will iterate over the last row's values.

Run the collection by hitting Start. You'll see the collection requests running in sequence and the results of your tests.

![[collection runner running requests](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen-running.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/ramen-running.png)