## Before you start...

Here we have the basic steps any merchant, marketplace or ecommerce platform should follow in order to take the best advantage from Wirecard's APIs.
The collections available in this document consider the most used business models and the main features Wirecard offers.

The documentation is divided in two basic integration scopes:

- Scope 1 - Ecommerce Integration | This model considers the necessary steps for any ecommerce to start creating transactions.

- Scope 2 - Marketplace/Platform Integration | This model considers the steps necessary to create splitted payments and/or create payment on behalf of other users.

The Scope 2 includes:

- Account onboarding;
- Split with marketplace as primaryReceiver;
- Split with marketplace as secondaryReceiver;
- Split with secondary as feePayor;
- Split with escrow;
- Split with multiorder (shared cart);
- Split with multiorder with escrow
- Payout

The onboarding and payout are pretty much the same for any marketplace or integrator that decides to use Wirecard as a payment service provider, but the payment flows can be quite different.

So, make sure you choose the one that best suits your business model.

# Terminology

## Ecommerce

Ecommerce term is related to any merchant or business model where the integration doesn't require payment splitting.

## Integrator

In most cases the integrator is a marketplace or an ecommerce platform that is creating payments for a merchant. However, this term applies to any agent who is using Wirecard to create or retrieve payments on behalf of other user.

## Primary Receiver 

The primary receiver is responsible for refunding transactions and has liability over chargebacks.
By default, the primary receiver is also who pays for Wirecard fees, however it is possible to define another `feePayor` when an order is created.

## Secondary Receiver:

The secondary receiver doesn't have liability over chargebacks and can't refund a transaction.
A marketplace can define that a secondary receiver will pay Wirecard fees by declaring the attribute `"feePayor":true` in the `order` request.

## OAuth APP

Sometimes can be refered as `channel` or `client`.
An APP OAuth represents a connector between an integrator and a merchant.
The use of that resource offers a lot of advantages, including:

- Safe authentication, using an accessToken that can be renewed or expired;
- Defining one unique (or many if you want to) notification preference for all merchants, so a merchant won't be able to change/delete it, breaking the integration;
- Different pricing setups (depending on Wirecard contract). This allows the integrator to offer different pricing setups for its customers, with different fees and settlement preferences;
- Different risk analysis rules in Wirecard's fraud prevention softwares;

# How to use this documentation

This documentation is intended to clarify some of the main business models our APIs can support.
As a merchant, a marketplace or an ecommerce platform, you will not need to integrate all of those models, you just need to identify the one that suits you best and go for it.

This collection is not an API Reference, nor it contains details about all API fields, however it offers a clear overview of the main topics you must follow in order to have a successul integration.

Anyway, if you need the API reference, there it goes: https://dev.moip.com.br/v2.0/reference

For now, our API reference is only available in portuguese.

# Account types

To have a smooth account onboarding a marketplace must take into consideration what's the experience it want to offer for its merchants.

Wirecard offers two types of accounts, allowing any marketplace or platform to create two different onboarding experiences, they are: Transparent Account and Classical Account.

|Transparent account      |Classical account     | 
|-------------------------|----------------------|
|Customized experience|Merchants have access to a Wirecard Account |
|Marketplace look and feel|Wirecard provides support for sellers|
|Full marketplace onboarding|Sellers can have their own Ecommerce and send invoices|
|Exclusive relationship with the sellers|Merchant can use any marketplace|
|Wirecard white label|Payout process through Wirecard Dashboard|


# Standard and Light Checkouts

As a payment provider we are concerned in making our APIs as flexible as possible at the same time we offer a highly secure platform with an advanced fraud prevention algorithm. That's why we created the ["Programa Venda Protegida"](https://suporte.moip.com.br/hc/pt-br/articles/115004708468-O-que-%C3%A9-o-programa-Venda-Protegida-e-como-ele-funciona-) (Secured Sales Program), in which we cover an amount of chargeback damage a merchant may have from credit card fraud.

Even thou most of the merchants we have as customers consider flexibility and fraud prevention important in equal measure, there's a huge amount of business models that tend to have a deeper need for one or another. Maybe you want to create payments with a really low set of customer's information even if it brings a higher fraud tendency, maybe you want to do anything you can to prevent frauds even if it has some impact on your UI and UX.

That's why we enhanced our APIs flexibility by creating the "Standard" and "Light" checkouts so we can help any business to get where they want. 
Standard and Light checkouts are not reallly different products, they are simply different combinations of customer's information sent when creating an `Order` in the API.

## Standard Checkout

The Standard Checkout is just the "business as usual" checkout version, it contains all the customer's details, offers the highest fraud prevention benefits and payments created within it are elegible to the ["Programa Venda Protegida"](https://suporte.moip.com.br/hc/pt-br/articles/115004708468-O-que-%C3%A9-o-programa-Venda-Protegida-e-como-ele-funciona-).
All `Order` and `Multiorder` requests in this documentation are using the Standard combination of attributes.

## Light Checkout

If the Standard checkout knows every customer attribute, the Light checkout only needs the minimum set of customer's data. Offering to  merchants the possibility to create really short checkout pages in their websites or mobile APPs. 
Payments created with the Light Checkout still goes through our fraud prevention systems and analysis, but as the missing information decreases their efficiency payments are not elegible to the ["Programa Venda Protegida"](https://suporte.moip.com.br/hc/pt-br/articles/115004708468-O-que-%C3%A9-o-programa-Venda-Protegida-e-como-ele-funciona-).

*IMPORTANT: We strongly recommend you to get in touch with our Support Team before using the Light Checkout. 
We can help you to analyze the impact it may have for your business and prevent unexpected behavior from your customers.*

### Checkout attributes combinations

| api-resource | attribute                            |standard|light|
|--------------|--------------------------------------|--------|-----|
| customers    | fullname                             | ✓      | ✓   |
| customers    | email                                | ✓      | ✓   |
| customers    | birthdate                            | ✓      |     |
| customers    | taxDocument.type                     | ✓      |     |
| customers    | taxDocument.number                   | ✓      |     |
| customers    | phone.countryCode                    | ✓      |     |
| customers    | phone.areaCode                       | ✓      |     |
| customers    | phone.number                         | ✓      |     |
| customers    | shippingAddress.street               | ✓      |     |
| customers    | shippingAddress.streetNumber         | ✓      |     |
| customers    | shippingAddress.district             | ✓      |     |
| customers    | shippingAddress.city                 | ✓      |     |
| customers    | shippingAddress.state                | ✓      |     |
| customers    | shippingAddress.country              | ✓      |     |
| customers    | shippingAddress.zipCode              | ✓      |     |
| payments     | creditCard.holder.name               | ✓      | ✓   |
| payments     | creditCard.holder.birthdate          | ✓      | ✓   |
| payments     | creditCard.holder.taxDocument.type   | ✓      | ✓   |
| payments     | creditCard.holder.taxDocument.number | ✓      | ✓   |


# Wallet transactions [*Beta*]

Wirecard also offers the possibility to create `payments` from Wirecard Account to Wirecard Account, that is what we call a `Wallet` payment.
This payment method works in a similar way to a `tranfer`, except that transfers generate a debit and a credit that have no relationship with an `order` or `multiorder`. The `wallet` payment looks exactly like a boleto or a credit card payment, they are always related and attached to an order and its content.

Also important to mention, the `wallet` as a payment method doesn't required the buyer to be redirected to a Wirecard Checkout, which means that any marketplace can offer its own user experience and user interface.

## Wallet as funding instrument

As described above, `wallet` payments are created in the same way boleto or credit card payments are, so all you need to do is to inform the `moipAccount.id` from the payor account in the `fundingInstrument` node in the payment request.

A `moipAccount.id` can be obtained in two ways, when you create a new account by using the APIs or by requesting an OAuth permission to a buyer.

## Two factor authentication

With the `moipAccount.id` you are in possession of the account main reference and identifier, now for every time you want to process a payment, you just need to require a confirmation from that customer/buyer that he actually is the owner of the Wirecard Account being debited.

That confirmation can be made through 2FA tokens, that can be obtained by the Wirecard Account APP (for Android) or SMS.

To validate tokens you should include the `customer-2fa-type` in the payment request header. To specify the type, use the parameters below:

| customer-2fa-type | Description | 
| ----------| ------------|
| `HOTP`    | `HMAC-based one time password`. Declares that the token included in the request header is "event-based" and was obtained by the buyer in a SMS|
| `TOTP`    | `Time-based one time password`. Declared that the token included in the request header was obtained by the buyer through Wirecard Android APP.


IMPORTANT: Our 2FA application follows the recommendations in the public [RFC](https://tools.ietf.org/html/rfc6238).

For more details, please look at the requests samples.

>IMPORTANT: Wallet payment can only be refunded in its full amount. In other words, it's not possible to create partial refunds for them.



# Changelog

| Date | Change |
| -----| ------| 
| 2017 | Documentation Created |
| 2018-Jan | Included Multiorder and Escrow. Changed the way the models are displayed. |
| 2018-Jun-15 | Included Standard and Light Checkouts | 
| 2018-Jul-10 | Included Wallet as a Beta transactional resource | 
| 2018-Jul-19 | Included the customer-2fa-token table for Wallet payments | 