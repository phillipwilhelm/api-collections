# Integrated Warehouse Tests

https://documenter.getpostman.com/view/6596490/TVRg8pzf

A collection of tests divided into parts, intended to test 3PLs that have already been integrated and set up in the Deliverr network.

To run this for a specific 3PL, fill in the `provider`, Deliverr `warehouseId`, and `testRun` number in the Variables tab:
- in Postman > Hover over the 3 dots for Warehouse API Tests > Edit > Variables tab.

For each iteration of the entire test collection here, a testRun number (in Variables) needs to be provided and incremented each time we want to run any test part more than once, so that we can re-run the same API calls and not have them conflict with one another.

To run a Test Part, click Runner in the top left corner of Postman, an d search for Test Part # (the test part that you want to run - remember that only 1 test part can be run at once). All tests in that test part will be selected by default. Select the environment you want to run in (generally this is `Staging`), and hit the big blue button `Run Warehouse API Tests`. 

The tests are divided into 3 parts - use the left hand column to navigate to instructions for each part:

| Test Part | Details |
| :--: | -- |
| 1 |<ul><li>Get Product Details</li><li>Create Product with valid and invalid details</li><li>Update Product (add barcode)</li><li>Get Asn Status</li><li>Create ASN</li></ul>|
| After 1 |<ul><li>Receive Asn Partially</li><li>Receive Asn Completely</li><li>Generate Inventory Movements</li></ul>|
| 2 |<ul><li>Get ASN Status</li><li>Get Inventory Movements</li><li>Get Inventory Status</li><li>Create Shipments (with multiple packages, with SIOC, with warehouse defined box name, with third party billing)</li><li>Cancel shipment</li><li>Get Shipment Status (processing and cancelled shipment status)</li></ul>|
| After 2 |<ul><li>Fulfill orders (shipment)</li><li>Cancel a shipment</li><li>Mark damaged units</li></ul>|
| 3 |<ul><li>Get Inventory Status</li><li>Get Shipment Status (fulfilled shipments with tracking codes)</li><ul>|