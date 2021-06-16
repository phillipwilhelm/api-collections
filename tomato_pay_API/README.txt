The tomato pay API platform, built by, and loved by developers, enables anyone to build exceptional financial products to serve small businesses.

By leveraging tomato pay's APIs such as our Open Banking, payments and intelligence APIs, you will gain valuable insights into your users finances so you can deliver the right product, to the right small business, at the right time.

<strong> Payments </strong>
<ul>
<li> Our payments API is built on the faster payment bank rails. It powers instant, cheaper and more secure payments without all the administrative burden. </li>
<li> Immediate settlement at a significant discount to cards, direct debit and other payment methods. </li>
<li> Secure authentication through a customer's own bank, reducing the risk of fraud. </li>
</ul>

<strong> Data Aggregation </strong>
<br> 
Through Open Banking, your customers can connect their bank accounts to get a holistic view of their finances.

<strong> Cash Flow Profiles </strong>
<ul>
<li> The core of our innovation lies in our ability to analyse your customers' aggregated financial data and enhance it with machine intelligence. </li>
<li> Produce cash flow forecasts, and surface automated insights. </li>
<li> Categorise your customers' transactions and provide timely, and valuable insights on their spending habits. </li>
</ul>

<strong> [Get your free API key developer.tomatopay.co.uk](https://developer.tomatopay.co.uk/signup) </strong> 

<h1> Open Banking APIs Status </h1>

Monitor the performance, availability and error rates of Open Banking APIs through a transparent and user-friendly dashboard.

<break>

<strong> [Click here to go see the status page](https://www.api.expert/industry/openbankingukproduction/) </strong>

<h1> API Reference </h1>

<h1> Changelog </h1>

<h2> May 2021 </h2>

<strong> [Bank Data API](https://docs.tomatopay.co.uk/#dc3900f5-721d-473c-bc67-20df026f09e2) </strong>

[Updated Retrieve Banks endpoint](https://docs.tomatopay.co.uk/#e09cc91a-1026-49a7-8447-83719f8d7865) 
- Added logos in PNG format
- Added AIS status and PIS status
- Added rdfName field (bank name)
- logoUrl field has been removed
- Added type as a query parameter to filter banks that support AIS and/or payments
- Renamed pg to pageId

[Updated Create Bank Consent endpoint](https://docs.tomatopay.co.uk/#9b156e2f-aba6-40d9-8677-30a0ec5abc36)
- Removed bankId from the path
- Added bankId to POST body
- Renamed 'permission' field to 'permissions'
- 'type' has been removed from the response
- Renamed 'signinUrl' to 'signInUrl'

[Updated Retrieve Bank Consents endpoint](https://docs.tomatopay.co.uk/#f9e0c6cf-e0e1-44c8-9420-b9e52b9dbcec)
- Removed bankId from the path
- Added bankId as a query parameter
- Added status
- Renamed 'permission' field to 'permissions'
- Removed 'dateCreated' for consent
- Removed 'ConsentType'

[Updated Retrieve Bank Consent (by id) endpoint](https://docs.tomatopay.co.uk/#9906a74a-e19d-4a3d-9d0a-a0fcba433f8b)
- Removed bankId from the path
- Added status
- Renamed 'permission' field to 'permissions'
- Removed 'dateCreated' for consent
- Removed 'ConsentType'

[Updated Put Bank Consent (by id) endpoint](https://docs.tomatopay.co.uk/#d7610153-0fea-43ba-a21c-7c8ee1e3ffa7)
- Removed bankId from the path
- Added bankId to POST body

[Updated Delete Bank Consent (by id) endpoint](https://docs.tomatopay.co.uk/#114be4ba-78f0-4ea2-802d-8c7bafd111c3)
- Removed bankId from the path

[Updated Retrieve Bank Accounts endpoint](https://docs.tomatopay.co.uk/#2758297c-b296-4103-ac38-b1b1b7bdd03c)
- Added consentId to the response for Open Banking accounts

[Updated Retrieve Bank Account (by id) endpoint](https://docs.tomatopay.co.uk/#b6556b0e-9cdb-4199-b372-589715f535a2)
- Added consentId to the response for Open Banking accounts

[Added Retrieve Parties endpoint](https://docs.tomatopay.co.uk/#6bce3b1e-f502-47f7-954b-d9bc78663a64)

<strong> [Payments API](https://docs.tomatopay.co.uk/#0ad76a6e-26bd-4766-a5bc-d85df73fd875) </strong>

[Updated Create Payment Consent endpoint](https://docs.tomatopay.co.uk/#37d4dda2-1b6e-415b-8dd5-1fa14836821c)
- companyId is now a mandatory header
- Changed the endpoint to /banking/v2/pay/domestic/consents
- Added bankId to POST body
- Renamed paymentType to type
- Renamed authUrl to signInUrl
- Renamed consentStatus to status

[Updated Authorise Payment Consent endpoint](https://docs.tomatopay.co.uk/#6615dfcf-7755-46a8-a909-0c85560c3c01)
- companyId is now a mandatory header
- Changed the endpoint to /banking/v2/pay/domestic/consents/:consentId
- Added bankId to POST body
- Renamed paymentId to ‘id’
- Added type (paymentType) to the response
- Renamed dateCreated to creationDate
- Added remittanceInfo to the response
- Added companyId to the response
- Renamed SchemeName to 'schemeName'
- Renamed Identification to identification
- Renamed Name to name
- Removed consentType

[Updated Retrieve Payment Consents endpoint](https://docs.tomatopay.co.uk/#080a2e69-7c21-42e5-b051-7660c63fad08)
- companyId is now a mandatory header
- Changed the endpoint to /banking/v2/pay/domestic/consents
- Renamed 'consentId' to ‘id’
- Added companyId to the response
- Renamed paymentType to type

[Updated Retrieve Payment Consents (by id) endpoint](https://docs.tomatopay.co.uk/#ae362f3b-3edb-42e1-97bb-e646c72607d8)
- companyId is now a mandatory header
- Changed the endpoint to /banking/v2/pay/domestic/consents/:consentId
- Renamed 'consentId' to ‘id’
- Added companyId to the response
- Renamed paymentType to type

[Updated Retrieve Payment (by id) endpoint](https://docs.tomatopay.co.uk/#f9961515-12f6-4917-91dc-38abe05e64b4)

- companyId is now a mandatory header
- Changed the endpoint to /banking/v2/pay/payments/:paymentId
- Added companyId to the response
- Renamed 'paymentId' to ‘id’
- Renamed date to creationDate
- Added remittanceInfo to the response
- Renamed paymentType to type
- Renamed SchemeName to 'schemeName'
- Renamed Identification to identification
- Renamed Name to name

[Added Retrieve Payment endpoint](https://docs.tomatopay.co.uk/#d75e5c28-f692-48b1-89b3-4b971904725e)


<h2> March 2021 </h2>

<strong> [Forecast API](https://docs.tomatopay.co.uk/#e55285f1-b329-40b0-972c-d3ae6d90d240) </strong>

<strong> Updated Forecast API endpoints </strong>

<break>

Removed bankId from the app and added bankId to the body and response (wherever relevant).

<h2> November 2020 </h2>

<strong> [Bank Data API](https://docs.tomatopay.co.uk/#dc3900f5-721d-473c-bc67-20df026f09e2) </strong>

[Updated Retrieve Bank Accounts endpoint](https://docs.tomatopay.co.uk/#2758297c-b296-4103-ac38-b1b1b7bdd03c)

[Updated Retrieve Bank Balances endpoint](https://docs.tomatopay.co.uk/#c6232c86-f254-4e48-9df9-543a4bd8d83a)

[Updated Retrieve Bank Transactions endpoint](https://docs.tomatopay.co.uk/#ed354431-80b0-4574-b3fc-b42dd87fbc78)

[Updated Create Consent endpoint](https://docs.tomatopay.co.uk/#9b156e2f-aba6-40d9-8677-30a0ec5abc36) Consent for retrieving specific data can now be requested

<li> Deprecated \banking\v2\banks\:bankId\accounts; use \banking\v2\accounts endpoint instead </li>
<li> Deprecated \banking\v2\banks\:bankId\balances; use \banking\v2\balances endpoint instead </li>
<li> Deprecated \banking\v2\banks\:bankId\transactions; use \banking\v2\transactions endpoint instead </li>
</ul>

<h2> October 2020 </h2>

<strong> [Company API](https://docs.tomatopay.co.uk/#7e079fc5-c37a-44aa-a7d0-b4865a79ed86) </strong>

[Added Update Company endpoint](https://docs.tomatopay.co.uk/#1695d206-b4fa-4052-83ce-d15b819e72bb)

[Updated Create Company endpoint](https://docs.tomatopay.co.uk/#73793898-d8ba-4e2d-b4aa-2d17737d5d27)
<ul>
<li> External ID and/or CRN can now be added to a company. </li>
<li> Added support for creating single company and multiple companies. </li>
</ul>

<break>

[Updated Get Companies endpoint](https://docs.tomatopay.co.uk/#d1c7e6cc-f772-454f-8968-20843639bd34)
Companies can be queried by External ID and/or CRN.