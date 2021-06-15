Kaleyra Hexa, the flagship product, allows developers, businesses and startups to code, build and scale their communication. At Hexa, we offer it all; right from SMS, Voice, Numbers, Instant Messaging and Emails.

# Hexa API
Introducing the powerful API that can seamlessly perform multiple functions in less than 5 milliseconds. We made it simple for you, with minimum coding and a multidimensional approach. 

You can download the [Postman collection for Hexa here](https://www.getpostman.com/collections/0f8cc583dd99b57e8f53)

# Login And Get API Key to get started

To get an API Key, you will have to create one by [logging in to our application](https://hexa.kaleyra.io/). The process is listed below: 

# Create an API Key

To create an API key, follow the steps below:

1. From the Hexa application, click on 'Dev Console'
2. Click on 'Create an API Key'
3. Enter the details and click 'Add' 

# API Parameters
The following are the API Parameters for Hexa APIs:

|Parameter Name |Description |
|---------- |-------------- |
|type |Type of SMS, i.e, marketing (MKT), transactional (TXN), One Time Passwords (OTP) |
|body |Message(s) to be sent |
|to |To phone number(s) |
|sender |Sender id|
|ref |Message reference tags |
|listid |Contact number groups |
|time |Time in the format dd-mm-yyyy hh:mm:ss |
|dlrurl |Delivery url |

# Parameter Combinations
> 'to' and 'listid' cannot be used in the same trigger. 'to' parameter will be priortized instead of 'listid', for both sending and scheduling the SMS.

> For OTP messages, only one mobile number can be added per request

# Mandatory Parameters
|Parameter Name |Description |
|---------- |-------------- |
|to |Mobile number(s) to which the SMS has to be sent |
|body|Message content |
|sender |Sender id |
|type |Type of the message (TXT, MKT, OTP)




# Error Codes
|Error Code |Description |
|--------- |---------- |
|E100 |Message Submitted Successfully |
|E101 |Campaign Accepted |
|E102 |No Medium Configured for Queue |
|E103 |Internal Server Error |
|E104 |No Records Found |
|E105 |Status Field is Mandatory |
|E400 |For bulk SMS type should be MKT |
|E401 |SMS length is exceeding '.Config('sms.max_length').' characters. |
|E402 |Message can be scheduled for after 15 minutes from current time and before 3 months from now |
|E403 |Something went wrong at our end please try again after some time |
|E404 |If Type is OTP then only one mobile number is allowed |
|E405 |If Type is TXN then mobile numbers should not be more than 100 |
|E406 |No Valid mobile numbers found |
|E407 |Sms nodes are mandatory in JSON API |
|E408 |to field is mandatory in each sms nodes |
|E409 |Maximum '.config('sms.json.max_limit').' sms nodes are allowed |
|E410 |To field cannot contain commas |
|E411 |To field has to be filled in sms nodes |
|E412 |Body has to be filled, Either in sms nodes or in global node |
|E413 |Invalid inputs, Validation error |
|E600 |To field has to be filled |
|E601 |Body cannot be left empty |
|E602 |Sender-Id is required |
|E603 |Port number must contain only numbers |
|E604 |Unicode should contain only 0, 1 or AUTO |
|E605 |Duplicate should contain only 1 or 0 |
|E606 |Flash should contain only 1 or 0 |
|E607 |Campaign name should contain only alpha numerics |
|E608 |ref should contain only alpha numerics |
|E609 |ref1 should contain only alpha numerics |
|E610 |ref2 should contain only alpha numerics |
|E611 |Type is required |
|E612 |For Group SMS Use Either 'to' field or 'list_id' field |
|E613 |List_id field has to be filled |
|E614 |For 'list_id' type should not be OTP |
|E615 |Type has to be either TXN, MKT or OTP |
|E616 |Sender field has to be filled |
|E617 |Campaign_id field has to be filled |
|E618 |Body field has to be filled |
|E619 |Invalid Sender ID Pattern |
|E620 |Campaign validated successfully |
|E621 |Invalid Sender ID Pattern |
|E622 |Invalid Sender ID Pattern |
|E623 |Transactional Route is not enabled for your account. |
|E624 |Default Route is not enabled for your account |
|E625 |Marketing Route is not enabled for your account |
|E626 |Request Completed Successfully |
|E638 |Upload the files |
|E639 |Upload only csv or pdf files |
|E640 |Upload files which are less than 1 MB |
|E641 |Source will contain minimum 3 characters and maximum 10 characters |
|E642 |Source has to be filled with only string |
|E700 |Unable to upload the file |