A simple RESTful interface is used to initiate the hosted payment form and receive a JSON transaction response.  The PIConnect HPF is built upon the TSYS platform and secured by TSEP (Tsys Secure Payment), for secure manual entry or web based transactions.

The basic transaction flow is as follows:  

* POST non-sensitve transaction data and retreive a PTK which is required to render the form
* Append the PTK to a static URL to render the HPF  

![alt text](https://paymentinnovators.com/wp-content/uploads/2018/01/hpf_screen.png)  

* Card Account Number, Expiration and CVV are entered on the form, and transaction processes
* PIConnect HPF offers three methods of retreiving the transaction response: responseURL, polling, or fetch.
  

----
>**REQUEST FIELDS**  

Field | Description | Format | M/O
--- | --- | --- | ---
method | CreditSale, CreditAuth, CreditCapture, CreditReturn, CreditVoid, GetToken, CloseBatch, ACHSale, ACHReturn | AN(25) | M
account | Payment Innovator's issued account # | N(10) | M
paysource | PHONE, INTERNET (for Credit Card) / BOC (for ACH) | caps A(25) | M
amount | transaction amount | N(9) n.nn | M
ticketid | ticket, receipt, invoice | ANC(18) | M
userid | clerk or system user | AN(25) | M
address | street address for AVS | ANC(25) | O
zip | zip code or postal code for AVS | ANC(15) | O
notifyemail | email address for transaction receipt | ANC(40) | O
firstname | cardholder first name | AN(25) | O
lastname | cardholder last name | AN(25) | O
notes | comments or notes | AN(25) | O
ccardlevel | LEVEL2 | AN(25) | M for level2
l2taxamount | tax amount | n.nn | M for level2
l2custcode | corp card customer id | AN(18) | M for level2
l2purchaseorder | purchase order number | N(18) | M for level2
token | secure token representing card# | ANC(16) | M for token transactions
expirationdate | mmyy | N(4) | M for token transactions
cardtype | VISA, MASTERCARD, DISCOVER, AMEX, JCB | AN(10) | M for token transactions  
softdescriptor | purchase description on cardholder statement | ANC(32) | O
stationid | station identifier | N(8) | O (must be 8 numeric)
responseurl | url for JSON response | ANC (50) | O (highly suggested)  

----
>**HOSTED PAYMENT FORM URL OPTIONS**  

URL | Description | Color
--- | --- | ---
https://pi-stage.com/hpf/hpf.php?ptk=xxxx | form mimicking a credit card with card# and expiration date |  n/a
https://pi-stage.com/hpf/hpfweb.php?ptk=xxxx  |  white web form with card#, expiration date and cvv | n/a
https://pi-stage.com/hpf/hpf.php?ptk=xxxx&css=color | colored web form with card# and expiration date | Red, Blue, Green, Yellow, Grey, Pink, Black
https://pi-stage.com/hpp/hpfweb.php?ptk=xxxx&css=color  | modernized white web from with card#, expiration date and cvv | n/a

----
>**RESPONSE FIELDS**  

Field | Description | Format
--- | --- | ---
TransactionResult | true (successful) / false (unsuccessful) | AN(18)
PTK | Pi transaction key (unique) | ANC(18) 
ResponseCode | processor specific response code | AN(18)
ApprovedAmount | confirmation of amount processed (check for partial approvals) | n.nn
TransactionID | transaction reference | AN(18)
AuthCode | approval/authorization code | AN(18)
Token | secure token representing card# | AN(16)
CardType | VISA, MASTERCARD, DISCOVER, AMEX, JCB | AN(10)
AccountNum | last 4 of card number | N(4)
ExpirationDate | mmyy | N(4)
TicketID | ticket, receipt, invoice | AN(18)
ResponseMsg | processor message (important to display for unsuccessful transactions | AN(25)
HostCode | processor code | AN(25)
Timestamp | time of transaction | N(16)
AvsResponse | A,E,N,R,S,U,W,X,Y,Z,G,B,C,D,I,M,P  | AN(2)
CvResponse | M,N,P,S,U | AN(2)
CardHolder | cardholder name from card-present transaction | AN(25)
BusinessId | PIConnect account number | N(10
UniqueId | unique transaction id | AN(25)
TransType | transaction type confirmation | AN(25)
EntryMode | CHIP, SWIPE, MANUAL, CONTACTLESS | AN(25)
RefNum | processor or device reference number | N(25)
SerialNo | device serial number or id | N(25)
AmountDue |   populated for partial approvals for some processors | n.nn
TipAmount | confirmation of tip amount | n.nn 
HostResponse | processor or device response | AN(25)
ExtraBalance | balance on certain card types | n.nn
CardBin | card bin range | N(6)
(Multiple EMV response fields) | Tc, Tvr, Aid, Tsi, Atc, AppLab, AppPN, lad, Arc, Cid, Cvm | AN(25)  

----
>**EXAMPLE RESPONSE**  

    {
    "TransactionResult": "true",
    "ResponseCode": "000000",
    "ApprovedAmount": 0.16,
    "TransactionID": "2",
    "AuthCode": "000000",
    "Token": "ItQFeKQPGojb5781",
    "CardType": "MASTERCARD",
    "AccountNum": "5781",
    "ExpDate": "0919",
    "TicketID": "11",
    "ResponseMsg": "OK",
    "HostCode": "0",
    "Timestamp": "20171215084308",
    "AvsResponse": null,
    "CardHolder": "SMITH/JOHN",
    "BusinessId": "1512672892",
    "UniqueId": "5a33df5a1a565",
    "TransType": "SALE",
    "EntryMode": "CHIP",
    "RefNum": "88888888",
    "SerialNo": "69000436",
    "AmountDue": "0",
    "TipAmount": "0",
    "CvResponse": null,
    "HostResponse": "DEMO APPROVED",
    "ExtraBalance": null,
    "CardBin": "524366",
    "Tc": "A0026",
    "Tvr": "0000008000",
    "Aid": "A0000000041010",
    "Tsi": "E800",
    "Atc": "0026",
    "AppLab": "MasterCard",
    "AppPN": null,
    "Iad": "16106060012200005C3D00000000000000FF",
    "Arc": "00",
    "Cid": "40",
    "Cvm": null
    } |