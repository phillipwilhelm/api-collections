CartRover is a platform that effortlessly connects your sales channels (carts & marketplaces) with your back-end OMS or WMS system. Integrate with CartRover once and leverage our library of ecommerce integations. [Learn More](https://www.cartrover.com/).

The CartRover Orders API is a RESTful service that performs all data communication in JSON format. The order of the fields you submit is not important and the order of fields returned is not guaranteed.

There are four different levels of API access: Cart, Merchant, Warehouse, Master. Each provides access to different endpoints listed in their sections below.

All API levels have separate access credentials but use the same authorization procedure and data formats for sending and receiving.

To be notified of API changes, please [join our API email group](https://groups.google.com/forum/#!forum/cartrover-api-updates).

To monitor the API status and uptime, [subscribe to our status page](https://status.cartrover.com/).

# Getting Help

If you have questions about the API, head over to the [CartRover Community](https://support.cartrover.com/portal/community/cartrover).

For general CartRover support and information [view our knowledgebase](https://support.cartrover.com/portal/kb/cartrover) where you can learn about CartRover and open support tickets.

When requesting API support please include your API User and the `X-CartRover-Process-ID` response header value for any specific requests you have made. We recommend you log this response header for every API request you make so that you have it for reference if you ever need to go back and ask about a specific call.

Check out the official [CartRover PHP Client](https://github.com/CartRover/cartrover-php). Just include it directly in your project, we've done all the work for you!

Additional unofficial CartRover Libraries:

* [Ruby Client](https://github.com/sifourteen/cartrover-ruby-client) by sifourteen

# Authentication

[How To Get CartRover API Keys](https://support.cartrover.com/portal/kb/articles/how-to-get-cartrover-api-keys)

Remember to keep your keys secret and secure. You can cycle your API keys in CartRover when viewing them, which will immediately invalidate the previous keys.

## Basic Auth

Pass your API User and Key using the [Basic Access Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) standard.

1. Concatenate the API user and key and place a colon in between: `api_user:api_key`
2. Base 64 encode this string
3. Pass it as a header in the following format: `Authorization: Basic BASE64ENCODEDSTRING`

# Errors

All endpoints will return errors in the following format.

| Field        | Data Type           | Description  |
| ------------ | ----------- | ----- |
| success_code | boolean | Always FALSE for an error |
| error_code | ENUM      | Invalid - Invalid/Missing data submitted <BR> Failure - Hard error like: Duplicate order <BR> RateLimit - Over API Limit |
| message | String      | Specific Error Message |

# Rate Limit

The CartRover API uses a [Leaky Bucket](https://en.wikipedia.org/wiki/Leaky_bucket) algorithm to manage API access. The bucket size is 100 calls, and they refill at rate of 1 call every 0.6 seconds. Currently the New Order API endpoint is NOT rate limited. If we see abuse of the API, all endpoints will be rate limited.

All endpoints that are rate limited will return the following header with each request. It contains the remaining number of API calls you can currently burst to:

> X-CartRover-Api-Minute-Hits-Remaining

If you go over your rate limit, the API will return a standard error with the following code and message:


```json
{
    "success_code": false,
    "error_code": "RateLimit",
    "message": "Over API Limit. Please slow down requests."
}
```

# Timestamps

Timestamp fields should be submitted to the API in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format in order to specify the timezone.

Timestamp fields returned by the API will be formatted in ISO 8601 and always be in the UTC timezone.

> 2018-08-27T02:24:58+00:00

If you are passing a timestamp as a GET parameter, **YOU MUST** encode the plus symbol (`+`) as `%2B`

# Order Charge Field Definitions

The definitions below are how CartRover uses and calculates price fields. If you do not follow this standard, CartRover cannot guarantee the price information the warehouse receives will be correct.

## Order Header Fields

**sub_total:** Sum of Order Line extended_amount fields.

* Does not include sales_tax, order_discount, or shipping_handling
* If loading orders, you may need to add the order_discount to the sub_total if the cart has one and doesn't include it in the sub_total.

**order_discount:** Total post-tax discount on order as a positive number.

* Overall order level post-tax discount passed from cart + (Sum of addl_discount from Order Lines)

**sales_tax:** Total tax on order

* If tax is set on Order Line this must match the sum of all order line tax fields. Most interfaces don't set tax on the order line.

**shipping_handling:** Total shipping charge for the order passed from cart. No relation to the order line shipping_surcharge field.

**grand_total:** sub_total + sales_tax + shipping_handling - order_discount

**balance:** Not used right now. Set to 0 or leave off completely.

## Order Line Fields

**quantity:** Number/Quantity of this product ordered.

**price:** Cost of a single item. Does not include taxes, discounts, or shipping charges.

**discount:** Pre-tax Discount amounts to be applied to EACH single item as a positive number.

**addl_discount:** Post-tax Discount amount to be applied to the total item line as a positive number.

**tax:** Taxes applied to the total quantity of the total items in this line.

**shipping_surcharge:** Extra shipping charges that were added because of the total items in this line.

**extended_amount:**  (price - discount) * quantity

* Does not take addl_discount or tax into account