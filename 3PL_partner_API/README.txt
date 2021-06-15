This spec describes the API that a 3PL partner needs to implement for integration with the Deliverr fulfillment system. The presumption is that the paths described here are preceded by a domain/path of the partner’s choice, and that all endpoints are implemented, including the [Deliverr Label API](https://documenter.getpostman.com/view/5508192/S11ByMoM?version=latest)

The API will need to be a real time API - ie Deliverr expects products and shipments to be immediately be available via an API query. All requests made to the API should be able to receive a response within 30 seconds (Deliverr has a layer that will cut off at 30 seconds resulting in a timeout).

The WMS will provide Deliverr with credentials to access the API that was implemented to the provided specifications documented here. Deliverr will create products, asns, orders, to the WMS, via the WMS’s new API.

# Usage
Deliverr will call these endpoints, hosted on the warehouse's system. The flow of the endpoint calls will look similar to:
1. Deliverr creates a product.
2. Deliverr may update a product (to update either it's barcode values, its cost or its tarirff code).
3. Deliverr sends an inbound ASN to the warehouse.
4. Deliverr periodically gets the ASN status (~6 hours) to process any updates from the warehouse. 
5. Deliverr gets the product details back from the warehouse to get the dimensions of the product (which the warehouse will take after inbounding the product the first time).
6. Deliverr gets the inventory status of a product.
7. Deliverr gets inventory movements for a specified date range (these movements include any inbound shipments, damages, returns, manual adjustments,...) every ~20 minutes to pick up any unexpected changes in inventory levels
8. Deliverr sends an outbound order to the warehouse.
9. Deliverr may cancel a shipment (before a predefined cut off time)
10. Deliverr periodically retrieves the shipment status (every ~30 minutes) for the outbound order until the shipment is marked as shipped. Alternatively, the WMS can push shipment status updates when the status changes from PROCESSING to SHIPPED or PROCESSING to CANCELLED.


# Authorization
Deliverr accepts HTTP Basic for authorization/authentication when communicating with a partner 3PL. 
This choice will be configured internally at Deliverr during integration setup.

# HTTP Statuses
The API should return 200 on success, 404 on any entity not found, 4XX on any user error, 5XX on any server error.