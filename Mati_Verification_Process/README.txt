The Mati allows you to programmatically verify your users, in an easy and fully customizable way. Mati is built to make your company KYC/AML compliant!
For more information visit [getmati.com](https://getmati.com/)

We offer two ways to execute our verification flow:

- Web or Mobile SDKs
- API

We strongly recommend to use our SDKs to verify your users, since Mati already puts a lot of energy into supporting most devices, old and new smartphones, giving out the best UI/UX. But if for some reason you can't use our SDKs, we have an official API with which can send us your users' data that we will verify.

- Whether you use our SDKs or API, we return the verification data via webhooks (see sections below).
- If you are going to integrate Mati using Javascript, we recommend to use:[ our package](https://www.npmjs.com/package/mati-verification-api "JS Library")


![Mati verification process](https://i.snipboard.io/vEiFbI.jpg) 

You can also go to our [flowchart](https://docs.google.com/drawings/d/1pEWc4Mr3bZVKYFh08BdFGVlZcbLaowcoGNbblwmcJP8/edit?usp=sharing) so you better understand how we verify users and what can you expect from each check.



# Mati Dashboard

You can customize your verification flow to best satisfy your business needs and your user base. It does not matter where they might be from, Mati supports their IDs. 

The forms of identification that we support are:

- National ID
- Passport
- Driver's License
- Proof of residence (i.e utility bills, bank statements, etc.)

You can select one or more documents to ask to your users. These can be as a sequence of different required documents or you can select more than one per step so your users can *choose* the one they currently have.

![Mati verification process](https://i.snipboard.io/x7Aiaj.jpg)

A flow with different document options

![Mati verification process](https://i.snipboard.io/tjhGmn.jpg) 



Additionally, you can add biometric verification to your flow, so that your user's face is matched with the photo in the identity card.

The forms of identification that we support are:

- A liveness requirement: It is a 7-second video in which the user is required to do 2 circles with his/her nose. This allows Mati to make sure that the user was really present at the time of verification.
![Mati verification process](https://i.snipboard.io/ICzQ6G.jpg) 

- A selfie photo: It is a simple photo of the user's face.
![Mati verification process](https://i.snipboard.io/D1SHq8.jpg) 

Both types of biometric will trigger a face-match check.


# Web SDK Overview

Our web SDK is executed through a customizable button. After you have configured your verification flow it will automatically synchronize through your `ClientID` from your dashboard and adapt to the settings you have selected there.

Watch the following video for a detailed explanation of the features of our Web SDK.
[![Web SDK Video tutorial](https://i.snipboard.io/ihUoEG.jpg)](https://www.youtube.com/watch?v=LH0A9qrqNkw&feature=youtu.be "Web SDK")

- Mati Web SDK is compatible with different frameworks: React, Angular and Vanilla JavaScript.

Implement it in your own website with just a few lines of code:
```
// Web SDK 
<script src="https://web-button.mati.io/button.js">
</script>
<mati-button
  clientid="CLIENT_ID" // from your Mati dashboard
  metadata='{"user_id":"1234778"}'
/>
```

Note that you should pass a metadata string as shown above, so you can know which user is being verified. This metadata string will be sent in all our webhook callbacks regarding to that verification in particular.

In your metadata strings you can pass:
- For email: please use the "email" field inside the metadata
- For any other information you want to send as metadata, feel free to use any characters 0-9, A-Z, a-z.

Also you can watch our web SDK integration logic tutorial below so you better understand how to configure your dashboard, use our button and how to interpret our webhook callbacks.

[![web SDK integration logic tutorial](https://i.snipboard.io/OA5wkW.jpg)](https://www.youtube.com/watch?v=Nmug8bynLN4&t=0s "Web SDK integration Video tutorial") 

You can also send a link to your users containing `metadata` strings, no website needed!

For example
```
https://signup.getmati.com/?merchantToken=YOURCLIENTID&metadata={"email":"example@mati.io","Client":"id3452"}
```

For more information regarding our button specifically please go to our [Github page](https://github.com/MatiFace/mati-web-button).

# iOS/Android SDKs integration

You can also verify your users through the usage of our mobile SDKs. See the following tutorial for full details.
[![Mobile SDK integration tutorial](https://i.ibb.co/Z1bgNYT/https-i-ytimg-com-vi-Tx4-ZJ8-AAk-ZA-maxresdefault.jpg)](https://www.youtube.com/watch?v=Tx4ZJ8AAkZA&t=1s "Mobile SDK integration Video tutorial") 

## iOS

- [Repo](https://github.com/MatiFace/mati-global-id-sdk/blob/master/Integration_iOS.md)
- [Tutorial](https://www.youtube.com/watch?v=sPS7_QoFhpY&t=0s)
- Minimum requirements: iOS 9.0, Xcode 10.2, Swift 5.0 

## Android

- [Repo](https://github.com/MatiFace/mati-global-id-sdk-integration-android)
- [Tutorial](https://www.youtube.com/watch?v=qDBjiBwyVF8&t=0s)
- Minimum requirements: Android v5.0 (API v21) or above 

# Other integrations

- [Ionic & Cordova](https://github.com/MatiFace/MatiGlobalIDSDKIonicCordova)
- [Xamarin](https://github.com/MatiFace/MatiXamarinIntegration)
- [React Native](https://github.com/MatiFace/react-native-mati-global-id-sdk)

# Webhooks - verification callbacks

For this section we recommend you to review our [flowchart document](https://docs.google.com/drawings/d/1pEWc4Mr3bZVKYFh08BdFGVlZcbLaowcoGNbblwmcJP8/edit?usp=sharing) so that you have a clear visual representation of all  the events that we will send you. Additionally, check out our video tutorial below.
[![Mobile SDK integration tutorial](https://i.snipboard.io/IJ4xqa.jpg)](https://www.youtube.com/watch?v=5uUbUdTkgYo&feature=youtu.be")

## Configure your webhook URL

Configure an `URL` to which Mati will send your user's webhooks in your dashboard inside the SDKs Integration tab
![Set Webhook URL](https://i.snipboard.io/chf9Nn.jpg). You can also set a `webhook secret` that we will use to hash out on of the headers in our webhooks, by decoding it using your `webhook secret` and comparing the decoded string you can always make sure that the webhook is coming from Mati and not another party.

Example of a decoding script:
```Java
const crypto = require('crypto');

// A sample webhook coming from Mati
const WEBHOOK_PAYLOAD = 
{   
    eventName: 'verification_completed',
    metadata: {email: 'john@gmail.com'},
    resource: 'https://api.mati.io/api/v1/verifications/db8d24783',
};

const MERCHANT_SECRET = 'your_mati_webhook_secret';

// Mati hashes your webhook payload
const signature = crypto.createHmac('sha256', MERCHANT_SECRET).update(JSON.stringify(WEBHOOK_PAYLOAD)).digest('hex');
console.log(signature);

function verify(signature, secret, payloadBody) {
    let hash = crypto.createHmac('sha256', secret);
    hash = hash.update(payloadBody).digest('hex');
    return hash === signature;
}

let isValidPayload;

isValidPayload = verify(signature, MERCHANT_SECRET, JSON.stringify(WEBHOOK_PAYLOAD));
console.log(isValidPayload);
```


For each verification that Mati has finished processing (via SDKs or API), Mati will send you a `verification_completed` webhook. Note that this webhook contains the key `matiDashboardUrl` which you can use to directly access a given verification through your browser.

All webhooks contain a `resource` URL that has all the user's verification information. Note that you do not have to wait for the `verification_completed` webhook to consult it. Just `GET` it! More information about this request in our `5 Retrieve verification data V1` section.

For every check that Mati performs, we will send you a corresponding webhook containing the result of said check.

The webhooks that we send are:
![Set Webhook URL](https://i.snipboard.io/OXYtMr.jpg) 

## Verification step errors

Note that if an error occurs in any of the verification `steps` we will send error key within the webhook with details about what went wrong.

For example:

```JSON
{
  "eventName": "step_completed",
  "step": {
    "status": 200,
    "id": "alteration-detection",
    "error": {
      "type": "LegacyError",
      "code": "legacy.error",
      "message": "Document is considered tempered"
    }
  },
  "resource": "https://api.getmati.com/api/v1/verifications/5e2b33d209b87d001bb72d6a"
}
```

Another example would be the case in which the user uploaded a document that is partially or completely unreadable. In this case Mati will return `null` for all `data`.
```JSON
{
    "status": 200,
    "id": "document-reading", 
    "data": {
        "fullName": {
            "value": null
        },
        "documentNumber": {
            "value": null
        },
        "dateOfBirth": {
            "value": null
        },
    },
}
```
In the case where the user verification has issues (ex: Mati could not read the ID document), we highly recommend that you manually check that user. That should not happen often, but you need to take it into account

Find an exhaustive list of `errors`, `messages` and their description in [this document document](https://docs.google.com/spreadsheets/d/1DRKhKoqskL44p-8TfnjA4E4ehWRE--8Dxpb1ZCI7e80/edit?usp=sharing)).

## Automating your flow with webhooks

After you have received the verification webhooks it is up to you to build rules to automate your user verification flow. (See our example integration logic inside our [flowchart document](https://docs.google.com/drawings/d/1pEWc4Mr3bZVKYFh08BdFGVlZcbLaowcoGNbblwmcJP8/edit?usp=sharing))

There is some little delay between the user finishing the Mati SDK, and Mati finishing to verify the user (usually a couple of minutes). During that time, we recommend that you display to your users a screen saying "We are verifying your identity, please come back in a few minutes". (Or any other business logic you would like to build with the information in our webhooks)

En example of an integrated verification process:

1) Let the user go through Mati SDK

2) Receive the frontend callback to know when the user finished the verification flow

3) Display a beautiful waiting page to the user saying "You are under review. Please come back in a few minutes!"

4) Wait for the `verification_completed` webhook, and parse the verification information

5) If there aren't any `error` inside Mati verification steps, automatically let your user access to your service

6) If Mati found some issues with the verification, you should probably manually check the user


# API Overview

This Postman collection allows you to explore the usage of the Mati API, so you can easily understand how to implement it in your own backend. It is important to note that these request should be performed sequentially so that the user verification process is successful. For step 3 `send-input`, 3 different configuration examples are shown for the convenience of the reader, step 3 should only be performed once per verification.

You can watch a video explanation of our API here:



[![API Video tutorial](https://i.snipboard.io/JzREkb.jpg)](https://www.youtube.com/watch?v=yD3zeC5WiO4 "API Video tutorial")


# Requests:
