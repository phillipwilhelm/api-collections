# Banking as a Service
Our vision is to collaboratively provide the underlying banking services infrastructure to fintechs and innovators in order to deliver best in class user experiences and target the next generation bank customers.

This suite of APIs provides access to an array of payment-related, enquiry & KYC lookup services. Vulte wraps around them an abstraction layer with one major goal: To provide a  consistent interface to integrators regardless of underlying service provider. That way, you can switch between providers at any time, based on quality of service, business justification, etc. without starting a new integration project or changing your systems in any way.


# Want to try it quickly?
To get started, sign up for Vulte by visiting https://openbanking.vulte.ng. Once your account has been approved, you will receive an invite email to set your password.
1. Set up your password
2. Login with newly set password
3. Generate your **API key** and **secret**
 


# Index of services
Here's the list of services available at the moment. It's a list that will grow with time as we complete more integrations.

## Lookup BVN Min
With this service, the calling apps can KYC a customer's bank verification number. This service will only return a True/False match of the supplied customer details if it matches what is saved against their BVN correctly.

## Lookup BVN Mid
With this service, the calling apps can do KYC with the customer's bvn. This service will return slightly above minimal KYC information.

## Lookup BVN Max
With this service, the calling apps can do KYC with the customer's bvn. This service will return maximum KYC information. 

## Lookup Account Min
With this service, the calling apps can KYC a customer's account numbe. This service will only return minimal KYC information. 

## Lookup Account Mid
With this service, the calling apps can do KYC with the customer's account number. This service will return slightly above minimal KYC information.

## Lookup Account Max
With this service, the calling apps can do KYC with the customer's account number. This service will return maximum KYC information.

## Get Statement
With this service, the calling apps can get statements of accounts. Apps will forward the customer reference account number they will like to obtain information on and forward to Vulte. 

## Get Balance
With this service, the calling apps can get available balance for a given source.
 
## Collect
With this service, the calling app can request or initiate payment from a customer. Provide a customer’s bank account number, Vulte forwards to selected provider, provider debits the linked account and credits beneficiary account tied to the app. The underlying provider may prompt for OTP, therefore you’d supply the OTP via a follow-on call. 
 
## Transfer Funds
With this service, the calling apps can do a transfer to a destination account number from a given source. Authorisation details (for source of funds) will always be required by the Vulte, apps will have to provide this.
 
## Disburse
With this service, the calling apps can do a transfer to a destination account number from a pre-configured account of the app. If authorisation details are required by a provider, apps will have to provide this.
 
## Lookup NUBAN
With this service, the calling apps can check corresponding banks matched to a customer's account number.  In effect, take an account number and try to determine which bank it’s from. 

## Get Accounts Min
With this service, the calling apps can take customer ref and return a masked list of accounts linked to it. Apps will collect the customer ref they will like to obtain information on and forward to Vulte.

## Get Accounts Mid
With this service, the calling apps can take customer ref and return an unmasked list of accounts linked to it. Apps will collect the customer ref they will like to obtain information on and forward to Vulte.

## Get Banks
With this service, the calling apps can get list of financial institutions with their corresponding codes. 

## List Branches
List branches of Polaris Bank

# Getting access to the APIs
To get started, sign up for Vulte by visiting https://openbanking.vulte.ng. Once your account has been approved, you will receive an invite email to set your password.
1. Set up your password
2. Login with newly set password
3. Generate your **API key** and **secret**

# General API information
The APIs are fairly RESTFUL and organized around the main services you would be interacting with. You can simply import this collection from the top right of the page into your **Postman**.

The base url currently sits at:

```
https://api.openbanking.vulte.ng
```


# Authentication headers
Authenticate your API calls by including your API key in the Authorization header of every request you make. You can manage your API keys from your dashboard.

***Sample Authorization Header:***
```
Authorization: Bearer {api_key}
```

Also, every request requires you to provide a unique `request-ref` per call. Then You'd need to add a custom header called `Signature` that's an MD5 hash of that `request-ref` and your `api-secret` separated by a semi-colon. `;`.

***Sample Signature Header:***
```
Signature:MD5Hash(request_ref;client_secret)
```

Your complete header for evey single call will look like:

	Content-Type:application/json
	Authorization:Bearer {{api_key}}
	Signature:{{MD5Hash(request_ref;client_secret)}}

# What requests would look like
For all requests, you'd put a JSON object in the body of your API call. All payloads have the following high level construct:

```json
	{
	  "request_ref":"0000000001",
	  "request_type":"lookup_bvn_max | get_statement |etc",
	  "auth": {
	    "type": "bvn | bank.account", 
	    "secure": "YKBOxtdD8kZHqG7JO0C9TZ",
	    "auth_provider": "Polaris"
	  },
	  "transaction": {
	    "amount": 10000,
	    "transaction_ref": "000001",
	    "transaction_desc": "A random transaction",
	    "transaction_ref-parent": "000001",
	    "customer":{
	    	"customer_ref": "000001",
	    	"firstname": "Kola",
	  		"surname": "Eboe",
	    	"email": "kolaebue@gmail.com",
	    	"mobile_no": "2348009871412"
	    },
	    "meta":{
	    	"a_key":"a_meta_value_1",
	    	"b_key":"a_meta_value_2"
	    },
	    "details": {
	    	"key": 'value'
	    }
	  }
	}
```

# What responses would look like
For all responses, you'd get a JSON object in the body of the response you receive. All payloads have the following high level construct:

```json
	{
	    "status": "Processing | WaitingForOTP | ProcessingOTP | Successful | Failed | OfflineValidating | OfflineValidated | OfflineNotifying | OfflineNotified",
	    "message": "The transaction has been processed successully",
	    "data": {
	    	"provider_responde_code":"00",
	    	"provider": "Polaris",
	        "errors": [],
	        "error": null,
	        "charge_token": "Kz5Dev7BenV9HmLNB",
	        "paymentoptions": []
	    }
	}
```

* **status**: Indicates the state of the request, whether successful, failed or anything in between
* **message**: Provides a text description of the state of the request and at times a message for the customer
* **data**: Will contain much more details of the outcome of the request. The values within this could vary by request type or endpoint called but some standard elements would be in almost all calls
* **provider_response_code**: The actual response code receieved from the underlyig provider, e.g. `00` for Quickteller
* **provider**: The provider that was used to process the request
* **errors**: In case of a failed transaction, this contains the lists of errors that occurred while processing the transaction
* **error**: This contain the most important error that hinders the successful completion of the transaction.
We highly recommend that developers use the Errors field to determine the result of an API call. As an empty Errors node indicate a successful transaction.


**NOTE**: Some API calls may have response elements that are only applicable to those API calls. You will see examples in the provided postman collection and across the documentation.

# Vulte standard status codes
* **Successful**: For  all requests that were successfully processed
* **Failed**: If a request fails. Read the errors object(s)
* **WaitingForOTP**: If a request requires OTP validation for completion.
* **PendingValidation**: If a request requires other information to be supplied for completion.
* **[Anything else]**: This would vary per endpoint called. Applicable values would be in the documentation for that endpoint.

# HTTP Status Codes
* **200**: A successful request occurred, do note that the description field on the response can contain further steps to be carried on this transaction
* **400**: Data validation error occurred due to inconsistent data supplied by the client
* **401**: Invalid request authorization, which might be due to invalid API key or the client is not registered for the service being accessed.
* **500**: An internal server error at our End, this should be reported if it persists.

# Encryption of Secure element
**NOTE** Please note that the underlying encryption behind the core Vulte communication is based on the AES algorithm. This section only shows encryption details for some parameters on the merchant request payload.

For encryption of values for the `auth.secure` field, do use Triple DES Encryption Algorithm with your application secret key as the encryption key 

E.g. 

```
TripleDES.encrypt("{bvn}",secretKey)
TripleDES.encrypt("{bank_account;bank_code}",secretKey)
TripleDES.encrypt("{otp}",secretKey)
```

**NOTE** Expiry date is MMyy

## Sample encryption in Java

	MessageDigest md = MessageDigest.getInstance("md5");
    byte[] digestOfPassword = md.digest(key.getBytes("UTF-16LE"));
 
    byte[] keyBytes = Arrays.copyOf(digestOfPassword, 24);
    
    for (int j = 0, k = 16; j < 8;) {
        keyBytes[k++] = keyBytes[j++];
    }
 
    SecretKey secretKey = new SecretKeySpec(keyBytes, 0, 24, "DESede");
 
    IvParameterSpec iv = new IvParameterSpec(new byte[8]);
    Cipher cipher = Cipher.getInstance("DESede/CBC/PKCS5Padding");
 
    cipher.init(Cipher.ENCRYPT_MODE, secretKey, iv);
 
    byte[] plainTextBytes = toBeEncrypted.getBytes("UTF-16LE");
    byte[] cipherText = cipher.doFinal(plainTextBytes);
 
    String output = new String(Base64.encodeBase64(cipherText));
 
    return output;

## Sample encryption in C-Sharp

	string encryptedText = "";
    MD5 md5 = new MD5CryptoServiceProvider();
    TripleDES des = new TripleDESCryptoServiceProvider();
    des.KeySize = 128;
    des.Mode = CipherMode.CBC;
    des.Padding = PaddingMode.PKCS7;

    byte[] md5Bytes = md5.ComputeHash(Encoding.Unicode.GetBytes(key));

    byte[] ivBytes = new byte[8];


    des.Key = md5Bytes;

    des.IV = ivBytes;

    byte[] clearBytes = Encoding.Unicode.GetBytes(TextToEncrypt);

    ICryptoTransform ct = des.CreateEncryptor();
    using (MemoryStream ms = new MemoryStream())
    {
        using (CryptoStream cs = new CryptoStream(ms, des.CreateEncryptor(), CryptoStreamMode.Write))
        {
            cs.Write(clearBytes, 0, clearBytes.Length);
            cs.Close();
        }
        encryptedText = Convert.ToBase64String(ms.ToArray());
    }

    return encryptedText;

## Sample encryption in PHP

	function EncryptV2($encryption_key,$data)
	{
	    $source = mb_convert_encoding($encryption_key, 'UTF-16LE', 'UTF-8');
	
	    $key = md5($source, true);
	
	    $key .= substr($key, 0, 8);
	
	     // a 128 bit (16 byte) key
	     // append the first 8 bytes onto the end
	
	
	    //Pad for PKCS7
	    $block = mcrypt_get_block_size('tripledes', 'cbc');
	    $len = strlen($data);
	    $padding = $block - ($len % $block);
	    $data .= str_repeat(chr($padding),$padding);
	
	
	
	    $iv =  "\0\0\0\0\0\0\0\0";
	
	    $encData = mcrypt_encrypt('tripledes', $key, $data, 'cbc',$iv);
	
	    echo base64_encode($encData);
	}

## Sample encryption in Node.js

	const crypto = require('crypto');

	function encrypt(sharedKey, plainText) {
		const bufferedKey = Buffer.from(sharedKey, 'utf16le');

		const key = crypto.createHash('md5').update(bufferedKey).digest();
		const newKey = Buffer.concat([key, key.slice(0, 8)]);
		const IV = Buffer.alloc(8, '\0');

		const cipher = crypto.createCipheriv('des-ede3-cbc', newKey, IV).setAutoPadding(true);
		return cipher.update(plainText, 'utf8', 'base64') + cipher.final('base64');
	}

    
# Switching providers for a service
All services subscribed to in your application are attached to providers that will end up fulfilling such service(s) on request. You can switch providers as you wish by managing the application from your dashboard and editing the service details. Also, for some endpoints, you can explicitly set the provider you would like to be used in the request payload. You would see examples in the documentation for the endpoints that support this.

# Bank CBN Codes
Anywhere bank codes are required in the API specification (bank_code), this refers to the CBN bank codes. Details of all bank codes can be found [here](https://bank.codes/api-nigeria-nuban/).



Now let's dive deeper into specific API calls.