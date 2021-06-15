This collection will check all the links on a webpage, crawl all internal links, and report broken links (if any).

Click the **Run in Postman** button to import the sample collection and environment template into your Postman app. You should now see the collection in the sidebar to the left and the environment selected in the dropdown in the top right.

  [![import collection and environment](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkImport.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkImport.png)

Get Started:
===
1. **Update environment**: Click the **Quick Look** icon in the top right to view and edit the environment variables. This is where you can update the values to check links on your own website. In many cases, your `root_url` will be the same as your `start_url`. However, in this example, we will use `https://learning.getpostman.com` as our `root_url`, and start checking links on `https://learning.getpostman.com/docs/postman/launching_postman/installation_and_updates`. 

    [![environment template](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkEnv1.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkEnv1.png)

2. **Open Postman Console**: This step is optional. If you want to see a stream of requests and view any logged statements, go to the application menu, and select `View` > `Show Postman Console` to open the console in a separate window. Do this before you send any requests or run the collection.

  [![Postman Console](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkConsole.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkConsole.png)
  
3. **Run collection**: Click the right angle bracket (**>**) to expand the collection details view. Click the **Run** button to open the collection runner in a separate window. 

  [![collection details](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkCollDetails.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkCollDetails.png)

  Verify that your collection and environment are selected in the respective dropdowns, and click **Start Run** to begin running your collection.
 
  [![collection runner](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkCollRun.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkCollRun.png)

You should now see your tests running and passing, crawling all the links until there are no more links to check.

  [![tests passing](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkCollRunner.png)](https://s3.amazonaws.com/postman-static-getpostman-com/postman-docs/linkCollRunner.png)