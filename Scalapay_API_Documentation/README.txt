![alt text](http://promotion.scalapay.com/templates-and-logos/API.jpg "Scalapay API flow")

# **API Documentation**
This is a basic description of how a Scalapay integration via our APIs would look from your site.

|**Environments**| URL |
| --- | ----------- |
|**Production**: | https://api.scalapay.com|
| **Staging**: |https://staging.api.scalapay.com|



## **Functional Order Flow**
1. Determine if your checkout should display Scalapay as a payment option.
2. Your site calls the [**/v2/orders/**](https://docs.api.scalapay.com/#f48967a6-6acc-4ce1-b812-b29d45eeb51f) endpoint to initiate the Scalapay payment process.
3. Then your site exectues the redirect to the [Scalapay checkout page](https://portal.scalapay.com/checkout?token=ORDER_TOKEN)
4. On the successful completion of the Scalapay pre-approval process, Scalapay will redirect back to the provided redirectConfirmUrl appending the token and a status of ‘SUCCESS’ OR 'FAILED’ as an HTTP query parameter.
5. Whenever your e-commerce platform creates the order, the site calls the [**/v2/payments/capture**](https://docs.api.scalapay.com/#942903b8-ba41-46ac-b8c2-ed764b6e66f8) endpoint to capture the payment and finalise the order.
6. ScalaPay finalises the consumers payment and responds with a success or a failure.


In order to acheive optimal success of installing Scalapay on your site then follow our
[Scalapay Installation Guidelines](https://scalapay.atlassian.net/servicedesk/customer/portal/2/topic/4853b78d-8412-4eb4-a44d-7160b179cdaa)


# Scalapay Widget

The Scalapay Widget is designed to provide the quickest intergration on the product and cart page of your online store.

Simply add the following lines of code to the bottom/footer of your product or cart HTML page:

```
<script src="https://cdn.scalapay.com/js/scalapay-widget/webcomponents-bundle.js"></script>
<script src="https://cdn.scalapay.com/js/scalapay-widget/scalapay-widget.js"></script>
```

Then place the widget in the desired location in the HTML of the product and cart page:

```
<div>
    <scalapay-widget amount="200"></scalapay-widget>
</div>
```

For further instructions and configuration items please visit the [Scalapay Widget] page

[Scalapay Widget]:
https://www.cdn.scalapay.com/js/scalapay-widget/

# API