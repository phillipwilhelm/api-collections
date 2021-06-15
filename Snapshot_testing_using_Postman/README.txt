To setup Snapshot Testing for your APIs you can use this collection as reference.
 1. Import the collection. Collection Test Script already contains all the script required for this.
 2. Send the request and get a response for the API you want to create a Snapshot test.
 3. Save the response as an Example to that request. This will work as your Snapshot.
 4. Create a Mock server on top of the collection.
 5. Update the `snapshotURL` in **Collection Variables** with the Mock server url that you created above.

This collection contains three different Snapshot testing strategies. You can choose any of them according to your use case and your response structure.