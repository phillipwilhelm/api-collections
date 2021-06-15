# 1 - About this documentation

This documentation references the Bit Capital platform APIs in their versions:

- API Core version: `3.0.x`
- API Core version: `2.x.x` for SaaS partners
-  **API PIX version: `0.4.3` for PIX partners - documentation in progress.*

<br /> 


The **BitCapital Core API** allows you to programmatically access data and resources from the Tokenization and Banking platforms, providing an easy way to access and manage financial resources and digital wallets in a fully regulated environment for Brazilian customers.

The easiest way to get started with the API is to click the Run in Postman button present at the top of the documentation page and use the **Postman App** to send requests.

For more information, check the [Bitcapital Developers](https://bitcapital.com.br/develoeprs) portal.

<br />

# 2 - PIX API


For our clients that optionally uses PIX Instant payment System, we offer a exclusive API at [https://bitcapital.stoplight.io/](https://bitcapital.stoplight.io/)
Please visit this website for this service.

<br />

# 3 - Understanding "your" platform
<br />

### Scopes and Roles


| role | function | scopes of permission |
| --- | --- | --- |
| `mediator` | the **highest possible level** of permission that the Bit Capital client has. This role can manage all domain of your environment.It is with this profile that the client will work to implement the development of his solution. The "mediator" credentials are delivered through an exchange of keys by the tech team of both teams. The Bit Capital services contractor is solely responsible for the security of this login acess credentials | [see the scopes in the login example link in this link ](https://docs.bitcapital.com.br/?version=latest#b73e76be-c6c1-4a2e-8434-ccfea50cc548)
| `consumer` | is the role for the consumer of the platform (the costumer). This profile is limited to changes to **your data only**, not allowing neither to search or edit any data others consumers than your own. All `consumer` accounts are managed by a `mediator` of the same `domain`| [see the scopes in the login example link in this link ](https://docs.bitcapital.com.br/?version=latest#b73e76be-c6c1-4a2e-8434-ccfea50cc548) |
| `audit` | this user has **read-only permission**. Assigned to audit team and compliance team.  | [see the scopes in the login example link in this link ](https://docs.bitcapital.com.br/?version=latest#b73e76be-c6c1-4a2e-8434-ccfea50cc548) |
| `operator` | designated for **basic operations** such as service desk service. It does not have access to sensitive consumer data.  | [see the scopes in the login example link in this link ](https://docs.bitcapital.com.br/?version=latest#b73e76be-c6c1-4a2e-8434-ccfea50cc548) |

<br />

### Infrastructure
Every application running inside the platform has its own container instance, isolated in the Bitcapital Cluster and accessible through a specific URL in the BT Core load balancers.<br>

> **Status and Maintenance:** All systems are monitored in real time, with performance, uptime and maintenance information being publicly available at: 
[https://status.btcore.app](https://status.btcore.app/)
<br>
#### Instances
We provide 2 development environments to your dev team, it's called ***instances***. These are **Testnet** and **Nighlty**.
Depending on the kind of contract with Bit Capital, we will make one or both available to you. Today, for partners who hire Banking services is avaliabe the **testnet** instance. For PIX partners, we provide the **nighltly** for your development.
***Tip: [see the Bit Capital Case in Google :)](https://cloud.google.com/customers/bit-capital?hl=pt-br)***
<br>
#### Domains
Domain is your domain! It's your space where you as a `mediator`credential can develop all strategies fo your banking solution. You as `mediator` has total permission inside your domain.  

<br />

### API client credentials

To start using this API you need both a **Client ID** and a **Client Secret**, emitted by the Bit Capital infrastruture team.
> #### **If you don't have yours yet, request the yours right now** at [https://developers.bitcapital.com.br/](https://developers.bitcapital.com.br/) or send a mail to hello[at]bitcapital.com.br or (if you are not a millenium) call us +55 11 4200-bit0

- **`API_BASE_URL`**: The instance URL in the load balancer. For example: ```https://testnet.btcore.app``` or ```https://nightly.btcore.app``` for PIX credentials.
- **`CLIENT_ID`**: The unique client ID that identifies the platform being used to access the API.
- **`CLIENT_SECRET`**: A non-expirable secret key, used to securely sign requests to the platform.


<br />

### Login with `mediator` credentials

As a partner application running inside the Bitcapital Platform, you'll be provided with a set of  Mediator credentials. It allows you to sign users up in the platform, validate their documents and handle all its financial resources.

<br />


```
curl --location --request POST 'https://testnet.btcore.app/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Basic ABEARERTOKEN' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username=emailmediator@email.com' \
--data-urlencode 'password=astrongpassword'
```

- **Email**: An email address to contact the mediator in the platform
- **Password**: A non-expirable secret key, to access the resources in the platform
- *** *username: a new kind of login avaliable only in Core v3.x.x***

<br/>

### Login with `consumer` credentials

A consumer is an account for the end-user to interact financially with the system. They are grouped into buckets called Domains, which hold some business logics and global limits.

<br />


```
curl --location --request POST 'https://testnet.btcore.app/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Basic ABEARERTOKEN' \
--data-urlencode 'grant_type=password' \
--data-urlencode 'username=mailconsumer@email.com' \
--data-urlencode 'password=astrongpassword'
```
<br />

- **Email**: An email address to identify the consumer in the platform, not communication will be send directly to the consumer
- **Password**: An optional passphrase to allow the consumer to interact directly with the BT Core APIs, performing operations without holding a mediator token.
- *** *username: a new kind of login avaliable only in Core v3.x.x***

<br />

### SDK Development


Some examples to develop using SDK.


#### Authenticating with client credentials
```
import Bitcapital from '@bitcapital/core-sdk';

// Initialize the session instance to authenticate
// using the Bitcapital Core OAuth 2.0 provider.
const bitcapital = Bitcapital.initialize({
  // Instance URL for REST API calls
  baseURL: 'https://your-instance.btcore.app',
  // Credentials for OAuth 2.0 requests
  clientId: '< YOUR CLIENT_ID HERE >',
  clientSecret: '< YOUR CLIENT_SECRET HERE >',
});

try {
  // Authenticate a client (API, service, etc) with the credentials from
  // the previous Bitcapital initialization method call.
  // If succeeds and available, the credentials will be stored in the 
  // session instance and in the local storage (for browser environments).
  const user = await bitcapital.session().clientCredentials();

  // The session returns a virtual user info and its credentials
  console.log(user.credentials.accessToken);

  // To logout and clear the current credentials, use the "destroy" action
  await bitcapital.session().destroy();

} catch(exception) {
  // Something went wrong, probably credentials are invalid
  console.error(exception);
}
```

<br />

### Issuing custom assets

```
import Bitcapital from '@bitcapital/core-sdk';

// Initialize the session instance to authenticate
// using the Bitcapital Core OAuth 2.0 provider.
const bitcapital = Bitcapital.initialize({
  // Instance URL for REST API calls
  baseURL: 'https://your-instance.btcore.app',
  // Credentials for OAuth 2.0 requests
  clientId: '< YOUR CLIENT_ID HERE >',
  clientSecret: '< YOUR CLIENT_SECRET HERE >',
});

try {
  // Authenticate a client (API, service, etc) with the credentials from
  // the previous Bitcapital initialization method call.
  // If succeeds and available, the credentials will be stored in the 
  // session instance and in the local storage (for browser environments).
  await bitcapital.session().clientCredentials();
	
  // List your asset in the platform
  const asset = await bitcapital.assets().create({
    name: 'My Awesome Personal Coin',
    code: 'MAPC',
  });

  // Emit some MAPC tokens to a specific wallet
  let transaction = await bitcapital.assets().emit({
    code: 'MAPC',
    amount: '10.00', // The amount to be credited
    destination: ' WALLET ID '
  });
  
  // P2P payment in MAPC tokens between two consumers
	transaction = await bitcapital.payments.pay({
  source: ' WALLET ID ',
  recipients: [{
    asset: 'MAPC',
    amount: '10.00',
    destination: ' WALLET ID '
  }];
    
  // Destroy some MAPC tokens from a specific wallet
  transaction = await bitcapital.assets().destroy({
    code: 'MAPC',
    amount: '10.00',
    source: ' WALLET ID '
  });


  // To logout and clear the current credentials, use the "destroy" action
  await bitcapital.session().destroy();

} catch(exception) {
  // Something went wrong, probably credentials are invalid
  console.error(exception);
}
```
<br />


### Getting Started

Start by authenticating in the platform using the **OAuth 2.0** protocol. Then, holding a valid access token, you can start by checking the current `domain` information. This is where your consumer accounts will be created and managed.


<br />


**- A simple way to verify if you are logged in the platform**

```bash
curl --location --request GET "https://testnet.btcore.app/users/me" \
  --header "Authorization: Bearer ABEARERTOKEN" \
```


<br />
**- Response of a creation of a `consumer` **

According to your Core version (v2 ou v3) the responses must be a little difference of each one. 

To view the responses, please follow the responses in the [**onboardidng section**](https://docs.bitcapital.com.br/?version=latest#a8cada24-8c2f-440a-a11a-05d5136cd11a).


<br />

# 4 - Schema responses

This section shows line by line the responses of the most common endpoints on the platform. We believe to be of great help to all developers. In addition, any questions do not hesitate to contact us.


### **Schema Response for `GET {{API_BASE_URL}}/users/:id` in Core v2**

```typescript
{
    "id": "c2c7436b-07a4-49bb-9ef5-11c47b6f5461", //the unique userId, the main Id of all users
    "status": "active", // the user state
    "name": "Name of Consumer", //concatenated from firstName + lastName
    "firstName": "Name",
    "lastName": "of Consumer",
    "email": "name.of.consumer0@gmail.com",
    "role": "consumer", // mediator | audit | operator | consumer
    "twoFactorRequired": false, // avaliable only on-demand
    "updatedAt": "2021-02-10T23:33:33.706Z", // ISO 8601
    "createdAt": "2021-02-10T23:33:33.706Z",  // ISO 8601
    "states": [ //states of a "user" arranged in timeline earlier to older
        {
            "id": "b54ec56c-e0d5-4c84-b1be-c3084e0b90c3",
            "status": "active", // 3rd pasristed state of user object
            "createdAt": "2021-02-10T23:33:51.426Z",
            "updatedAt": "2021-02-10T23:33:51.426Z",
            "additionalData": {}
        },
        {
            "id": "06a57276-d108-4a81-adf5-ff8b11f3243c",
            "status": "processing", //2nd persisted state of user object
            "createdAt": "2021-02-10T23:33:33.895Z",
            "updatedAt": "2021-02-10T23:33:33.895Z",
            "additionalData": {}
        },
        {
            "id": "e9f07df8-5f27-4bc0-8272-04b1aba26ba2",
            "status": "pending", // 1st persisted state of user object
            "createdAt": "2021-02-10T23:33:33.710Z",
            "updatedAt": "2021-02-10T23:33:33.710Z",
            "additionalData": {}
        }
    ],
    "wallets": [
        {
            "id": "a7e56ab1-5e9c-4981-a64a-989483632149", //identification of walletID
            "states": [ //states of a "wallet" arranged in timeline earlier to older
                {
                    "id": "1f64e299-3c98-41a5-8e65-6dea10988777",
                    "status": "ready",  // 5th pasristed state of user object
                    "createdAt": "2021-02-10T23:33:51.283Z",
                    "updatedAt": "2021-02-10T23:33:51.283Z",
                    "additionalData": {}
                },
                {
                    "id": "30cc4e1c-974d-40cf-8de6-f5eb4fb1d5c5",
                    "status": "pending_provider_approval",  // 4th pasristed state of user object
                    "createdAt": "2021-02-10T23:33:51.051Z",
                    "updatedAt": "2021-02-10T23:33:51.051Z",
                    "additionalData": {}
                },
                {
                    "id": "14b7bcf2-5bcb-460a-aaec-5a5e794d7a60",
                    "status": "registered_in_provider",  // 3rd pasristed state of user object
                    "createdAt": "2021-02-10T23:33:46.018Z",
                    "updatedAt": "2021-02-10T23:33:46.018Z",
                    "additionalData": {}
                },
                {
                    "id": "9f844a3c-6eaf-487b-abdb-2ce2ebcb6fd6",
                    "status": "registered",  // 2nd pasristed state of user object
                    "createdAt": "2021-02-10T23:33:36.020Z",
                    "updatedAt": "2021-02-10T23:33:36.020Z",
                    "additionalData": {
                        "transaction": "162ffc98-e04b-400c-9669-84b84b829578",
                        "hash": "9ba8bda7465b592ee610f51b257dd3120cc3e14e50ff7c915820469882bca875"
                    }
                },
                {
                    "id": "c8c12a02-cb58-45e7-ada3-6ab62e138d07",
                    "status": "pending",  // 1st pasristed state of user object
                    "createdAt": "2021-02-10T23:33:33.735Z",
                    "updatedAt": "2021-02-10T23:33:33.735Z",
                    "additionalData": {
                        "acceptProviderLegalTerms": true,
                        "fingerprint": "PostmanRuntime/7.26.8#::ffff:10.142.15.240"
                    }
                }
            ],
            "stellar": {
                "publicKey": "GDHSJMK7PUEVRFGFFFFH6A3WCAHL7I3ZWR5HER3HKNRISNO7GXXIZRYH" //publicKey in Stellar blockchain
            },
            "updatedAt": "2021-02-10T23:33:33.732Z",
            "createdAt": "2021-02-10T23:33:33.732Z",
            "deletedAt": null,
            "status": "ready",  // persisted status of wallet
            "additionalData": {} // additional data if necessary
        }
    ],
    "consumer": { //consumer has all personal data of a user
        "id": "4fc0324c-2e23-4c72-9b09-c2d912be3213", // the consumerId (not the main id of platform)
        "birthCity": "Sao Paulo",
        "birthState": "SP",
        "birthday": "1980-02-29T12:00:00.000Z", //ISO 8601
        "motherName": "Mae do user PF", 
        "civilStatus": "single", // single | married | divorced
        "financialProfit": "100.00", //string with dot separator
        "financialEquity": "100.00", //string with dot separator
        "type": "personal", // personal | corporate
        "pep": false, // political exposure
        "taxId": "12345678912", // cpf | cnpj
        "status": "ready", // last persisted status of consumerId 
        "states": [ //states of "consumer" arranged in timeline earlier to older
            {
                "id": "601ef672-4c5a-4d9b-888b-003b97f2c384",
                "status": "ready", // 7th persisted state of user object
                "createdAt": "2021-02-10T23:33:51.461Z",
                "updatedAt": "2021-02-10T23:33:51.461Z",
                "additionalData": {}
            },
            {
                "id": "b81642f5-8a1c-4411-b7ec-c95c624d8351",
                "status": "pending_billing_plan_subscription", // 6th persisted state of user object
                "createdAt": "2021-02-10T23:33:51.315Z",
                "updatedAt": "2021-02-10T23:33:51.315Z",
                "additionalData": {}
            },
            {
                "id": "4c89c87c-fe89-4257-892f-91110449844e",
                "status": "processing_provider_documents", // 5th persisted state of user object
                "createdAt": "2021-02-10T23:33:51.091Z",
                "updatedAt": "2021-02-10T23:33:51.091Z",
                "additionalData": {}
            },
            {
                "id": "0b12c0f5-b751-450c-a4bc-5d0a6af65c82",
                "status": "processing_wallets", // 4th persisted state of user object
                "createdAt": "2021-02-10T23:33:34.149Z",
                "updatedAt": "2021-02-10T23:33:34.149Z",
                "additionalData": {}
            },
            {
                "id": "19d89969-9ba3-4a25-b3ab-02e209debc25",
                "status": "pending_legal_acceptance", // 3rd persisted state of user object
                "createdAt": "2021-02-10T23:33:34.007Z",
                "updatedAt": "2021-02-10T23:33:34.007Z",
                "additionalData": {}
            },
            {
                "id": "f2b54505-57ea-40b3-94db-fa2f4bd1bbbc",
                "status": "processing_documents", // 2nd persisted state of user object
                "createdAt": "2021-02-10T23:33:33.932Z",
                "updatedAt": "2021-02-10T23:33:33.932Z",
                "additionalData": {}
            },
            {
                "id": "15ca977a-9e5e-4113-a26a-7e3e3e319397",
                "status": "pending_documents", // 1st persisted state of user object
                "createdAt": "2021-02-10T23:33:33.715Z",
                "updatedAt": "2021-02-10T23:33:33.715Z",
                "additionalData": {}
            }
        ],
        "updatedAt": "2021-02-10T23:33:51.461Z",
        "createdAt": "2021-02-10T23:33:33.713Z",
        "phones": [
            {
                "default": true, // at least one must be st defeult to be the number to be validadet by sms
                "id": "b1140153-2a52-43af-a73a-7b65a8c9909e",
                "number": "999888999",
                "code": "27",
                "countryCode": "55",
                "fullNumber": "+5527999888999", //concatenated field
                "verifiedAt": "2021-02-10T23:50:33.728Z", //if "null" means the phone is not validated yet
                "updatedAt": "2021-02-10T23:33:33.728Z",
                "createdAt": "2021-02-10T23:33:33.728Z"
            }
        ],
        "addresses": [
            {
                "id": "6b96b768-19e7-4cdd-bce6-9d4f3f27aa9a",
                "status": "own",
                "default": true, // at least one must be st default to receive the physical card
                "reference": "pto de referencia",
                "country": "BR",
                "state": "ES",
                "city": "Vitoria",
                "code": "29018280",
                "neighborhood": "Centro",
                "complement": "casa 01",
                "number": "100",
                "street": "Parque Moscoso",
                "updatedAt": "2021-02-10T23:33:33.720Z",
                "createdAt": "2021-02-10T23:33:33.720Z"
            }
        ]
    },
    "domain": { //domain of the user
        "id": "1294999d-c4c1-412a-933a-2b5c750593a4", //the domain of the user is in
        "name": "Bit Capital Network", //name of the domain
        "role": "root" // type os domain, default is "commom"
    }
}
```

<br />


### **Schema Response for `GET {{API_BASE_URL}}/users/:id` in Core v3**

```
{
    "id": "31224b73-5b26-4cac-b74e-e30ef1f99384",
    "status": "active", // the user state
    "name": "User Name", //concatenated from firstName + lastName
    "firstName": "User Name",
    "lastName": "Name",
    "username": "emailuser@email.com", //for best practice, it must be the same as email field
    "email": "emailuser@email.com",
    "role": "consumer",  // mediator | audit | operator | consumer
    "twoFactorRequired": false, // avaliable only on-demand
    "updatedAt": "2021-03-19T17:58:03.963Z",
    "createdAt": "2021-03-17T15:27:13.298Z",
    "states": [ //states of a "user" arranged in timeline earlier to older
        {
            "id": "d096f915-8e47-442c-8a90-24a4b4074fb7",
            "status": "active",  // 3rd persisted state of object
            "createdAt": "2021-03-17T15:27:17.223Z",
            "updatedAt": "2021-03-17T15:27:17.223Z",
            "additionalData": {
                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-5qv6k"
            }
        },
        {
            "id": "c378e88c-3d61-4fc2-801f-6e1f580fd3c1",
            "status": "processing",  // 2nd persisted state of object
            "createdAt": "2021-03-17T15:27:15.852Z",
            "updatedAt": "2021-03-17T15:27:15.852Z",
            "additionalData": {
                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-5qv6k"
            }
        },
        {
            "id": "6b599e5f-e9cf-49ab-b740-a4228d1c7be7",
            "status": "pending",  // 1st persisted state of object
            "createdAt": "2021-03-17T15:27:13.305Z",
            "updatedAt": "2021-03-17T15:27:13.305Z",
            "additionalData": {}
        }
    ],
    "wallets": [
        {
            "id": "c2f15407-a567-4795-9f4d-a4dffcc40ae6",
            "status": "ready", //transient status of wallet
            "states": [
                {
                    "id": "712fe93f-aabe-48f7-858d-4dfe4068044e",
                    "status": "registered", // 2nd persisted state of object
                    "createdAt": "2021-03-17T15:27:17.217Z",
                    "updatedAt": "2021-03-17T15:27:17.217Z",
                    "additionalData": {
                        "transaction": "ea278329-1a5a-454f-a898-54b079a3e0b8",
                        "hash": "fab7e0a36eb0ef5b4c27b4eb2897eb57225916c4a56e4718a1fb08982dd73455"
                    }
                },
                {
                    "id": "92d488c8-3455-45de-90aa-1b87485e7ed9",
                    "status": "pending", // 1st persisted state of object
                    "createdAt": "2021-03-17T15:27:13.517Z",
                    "updatedAt": "2021-03-17T15:27:13.517Z",
                    "additionalData": {}
                }
            ],
            "stellar": {
                "publicKey": "GA7S2HWITAOMQORM6KOWFZTBZ3GSVF5ZFRNDHYJJBP7XXM54GHSCJP63"
            },
            "updatedAt": "2021-03-17T15:27:13.498Z",
            "createdAt": "2021-03-17T15:27:13.498Z",
            "deletedAt": null,
            "assetRegistrations": [
                {
                    "id": "b21ea196-c91d-4741-b5ab-bfe9ba5f42f4",
                    "status": "ready",  //transient status of asset required:true
                    "asset": {
                        "id": "33b986c9-23ee-4262-ada7-0c9ed1b07b66",
                        "name": "BRL Parati", //name of asset
                        "code": "BRLP", //assetCode of asset
                        "root": true, // main asset of user
                        "required": true, // it means this asset is required dy default
                        "provider": "parati-provider" // provider of this service
                    },
                    "reportId": "3198e092-73e5-48fe-83ce-11f1085dc82a", //Id of compliance report for this asset
                    "createdAt": "2021-03-17T15:27:13.620Z",
                    "updatedAt": "2021-03-17T15:27:13.283Z",
                    "deletedAt": null,
                    "states": [
                        {
                            "id": "f1220b16-c4b3-47c4-9600-2e1d84d3d197",
                            "status": "ready", // 7th persisted state of object
                            "createdAt": "2021-03-17T15:43:02.960Z",
                            "updatedAt": "2021-03-17T15:43:02.960Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-5qv6k"
                            }
                        },
                        {
                            "id": "0f8e1d5a-980f-4cf2-ba31-215d182efee6",
                            "status": "approved", // 5th persisted state of object
                            "createdAt": "2021-03-17T15:43:00.086Z",
                            "updatedAt": "2021-03-17T15:43:00.086Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-dpzwb"
                            }
                        },
                        {
                            "id": "c7257560-49bd-4e2b-bd3f-5b1fad9863ac",
                            "status": "processing", // 4th persisted state of object
                            "createdAt": "2021-03-17T15:42:58.461Z",
                            "updatedAt": "2021-03-17T15:42:58.461Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-dpzwb"
                            }
                        },
                        {
                            "id": "0801ee90-69a7-4228-bbc3-33d8f182dfa2",
                            "status": "processing", // 3rd persisted state of object
                            "createdAt": "2021-03-17T15:42:58.453Z",
                            "updatedAt": "2021-03-17T15:42:58.453Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-dpzwb"
                            }
                        },
                        {
                            "id": "44b206c4-a5d4-4512-b180-c07224810d0e",
                            "status": "pending_documents", // 2nd persisted state of object
                            "createdAt": "2021-03-17T15:27:13.821Z",
                            "updatedAt": "2021-03-17T15:27:13.821Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-server-785c7c85f-59rhr"
                            }
                        },
                        {
                            "id": "ff128e54-f7c9-4d69-a016-74b7ecf705d8",
                            "status": "pending_registration", // 1st persisted state of object
                            "createdAt": "2021-03-17T15:27:13.639Z",
                            "updatedAt": "2021-03-17T15:27:13.639Z",
                            "additionalData": {}
                        }
                    ]
                },
                {
                    "id": "5af3d3fc-f225-4464-866f-1a839fac9d5e",
                    "status": "ready", //transient status of this asset
                    "asset": {
                        "id": "150e9076-72cb-43b5-a3db-956f7584c422",
                        "name": "Test Coin", //name of asset
                        "code": "TCN", //assetCode of asset
                        "root": false, // is not main asset of user
                        "required": false, // it means this asset is not required dy default
                        "provider": null // provider of this service
                    },
                    "reportId": null, // this asset has not required compliance check
                    "createdAt": "2021-03-17T15:27:13.835Z",
                    "updatedAt": "2021-03-17T15:27:13.835Z",
                    "deletedAt": null,
                    "states": [
                        {
                            "id": "32b09de7-b3e6-4fa1-87a5-6d474372c668",
                            "status": "ready", // 3rd persisted state of object
                            "createdAt": "2021-03-17T15:27:21.954Z",
                            "updatedAt": "2021-03-17T15:27:21.954Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-dpzwb"
                            }
                        },
                        {
                            "id": "626ed6f0-6333-45a5-83f5-dcd14f4ed96e",
                            "status": "approved", // 2nd persisted state of object
                            "createdAt": "2021-03-17T15:27:14.496Z",
                            "updatedAt": "2021-03-17T15:27:14.496Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-5qv6k"
                            }
                        },
                        {
                            "id": "6bec3a68-bcae-45dd-b458-87638c9e1bef",
                            "status": "pending_registration", // 1st persisted state of object
                            "createdAt": "2021-03-17T15:27:13.850Z",
                            "updatedAt": "2021-03-17T15:27:13.850Z",
                            "additionalData": {}
                        }
                    ]
                },
                {
                    "id": "d100e159-633d-46a2-a4bb-c0be05a9acfa",
                    "status": "ready", //transient status of this asset
                    "asset": {
                        "id": "63f4af75-8bfb-4925-ade0-265337770297",
                        "name": "BRL Bs2", //name of asset
                        "code": "BRLB", //assetCode of asset
                        "root": false, // it is not main asset of user
                        "required": false, // it means this asset is not required by default
                        "provider": "bs2" // provider of this service
                    },
                    "reportId": null, // this asset has not required compliance check
                    "createdAt": "2021-03-17T15:27:13.891Z",
                    "updatedAt": "2021-03-17T15:27:13.891Z",
                    "deletedAt": null,
                    "states": [
                        {
                            "id": "e1f94265-485f-46a9-83bf-2552c4565982",
                            "status": "ready", // 3rd persisted state of object
                            "createdAt": "2021-03-17T15:27:21.952Z",
                            "updatedAt": "2021-03-17T15:27:21.952Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-5qv6k"
                            }
                        },
                        {
                            "id": "fbb799f7-f94a-495f-8bdc-8c755af33ea8",
                            "status": "approved", // 2nd persisted state of object
                            "createdAt": "2021-03-17T15:27:15.369Z",
                            "updatedAt": "2021-03-17T15:27:15.369Z",
                            "additionalData": {
                                "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-dpzwb"
                            }
                        },
                        {
                            "id": "62cb8104-d03c-4440-b1fa-49760b6a2db7",
                            "status": "pending_registration", // 1st persisted state of object
                            "createdAt": "2021-03-17T15:27:13.917Z",
                            "updatedAt": "2021-03-17T15:27:13.917Z",
                            "additionalData": {}
                        }
                    ]
                }
            ],
            "assets": [ //a object that resumes all assets for this user
                {
                    "id": "33b986c9-23ee-4262-ada7-0c9ed1b07b66",
                    "name": "BRL Parati",
                    "code": "BRLP",
                    "root": true,
                    "required": true,
                    "provider": "parati-provider"
                },
                {
                    "id": "150e9076-72cb-43b5-a3db-956f7584c422",
                    "name": "Test Coin",
                    "code": "TCN",
                    "root": false,
                    "required": false,
                    "provider": null
                },
                {
                    "id": "63f4af75-8bfb-4925-ade0-265337770297",
                    "name": "BRL Bs2",
                    "code": "BRLB",
                    "root": false,
                    "required": false,
                    "provider": "bs2"
                }
            ],
            "additionalData": {
                "acceptProviderLegalTerms": true,
                "fingerprint": "PostmanRuntime/7.26.10#35.237.4.70" //the fingertip of "pending_legal_terms" acceptance
            }
        }
    ],
    "consumer": {
        "id": "400f5836-bfbe-40c2-a961-9be96bc884b7", //id of consumer ( it is not the main Id of user)
        "birthCity": null, 
        "birthState": null,
        "birthday": "1980-02-29T00:00:00.000Z",
        "motherName": "Mae do userPF",
        "civilStatus": "single",
        "financialProfit": "1000.00",
        "financialEquity": "1000.00",
        "type": "personal",
        "pep": false,
        "taxId": "08538995766",
        "status": "ready",
        "states": [
            {
                "id": "584aaa09-7e26-4850-888c-a41326f8e903",
                "status": "ready",
                "createdAt": "2021-03-17T15:27:17.500Z",
                "updatedAt": "2021-03-17T15:27:17.500Z",
                "additionalData": {
                    "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-5qv6k"
                }
            },
            {
                "id": "f6a7c3b7-a53d-478a-a5e1-64a85b5a587c",
                "status": "pending_billing_plan_subscription",
                "createdAt": "2021-03-17T15:27:16.403Z",
                "updatedAt": "2021-03-17T15:27:16.403Z",
                "additionalData": {
                    "pod": "nightly-core-core-api-consumer-workers-6fdb854df7-5qv6k"
                }
            },
            {
                "id": "5f9bf03f-5551-47d8-aa8a-001bb2b5eb27",
                "status": "pending_legal_acceptance",
                "createdAt": "2021-03-17T15:27:13.325Z",
                "updatedAt": "2021-03-17T15:27:13.325Z",
                "additionalData": {}
            }
        ],
        "updatedAt": "2021-03-17T15:27:17.500Z",
        "createdAt": "2021-03-17T15:27:13.318Z",
        "phones": [
            {
                "default": true,
                "id": "a86ca4ff-2b42-41a6-822e-1dcd7eb2bf03",
                "number": "888555444",
                "code": "27",
                "countryCode": "55",
                "fullNumber": "+5527888555444",
                "verifiedAt": null,
                "updatedAt": "2021-03-17T15:27:13.438Z",
                "createdAt": "2021-03-17T15:27:13.438Z"
            }
        ],
        "addresses": [
            {
                "id": "ab36107a-cc95-4f16-9287-cce1a2d5c642",
                "status": "own",
                "default": true,
                "reference": "pto de referencia",
                "country": "BR",
                "state": "ES",
                "city": "Vitoria",
                "code": "29018280",
                "neighborhood": "Centro",
                "complement": "casa 01",
                "number": "100",
                "street": "Parque Moscoso",
                "updatedAt": "2021-03-17T15:27:13.423Z",
                "createdAt": "2021-03-17T15:27:13.423Z"
            }
        ]
    },
    "domain": {
        "id": "7f717a62-a2d2-4fec-a8aa-ce2b2dbbdf4e",
        "name": "NOSSO DOMINIO",
        "role": "common"
    }
} 
```

<br />



### **Schema response for `GET {{API_BASE_URL}}/wallets/:id` in Core v2**


```
{
    "id": "e744b6f8-ecb4-4e32-8cd1-d199d100a5e3", //walletID
    "status": "ready", // transient sattus of wallet
    "states": [
        {
            "id": "807235c8-3bc4-4e0d-834a-a60ec56cc9eb",
            "status": "registered", //2nd persisted status of wallet
            "createdAt": "2021-03-24T13:15:11.038Z",
            "updatedAt": "2021-03-24T13:15:11.038Z",
            "additionalData": {
                "transaction": "196a2109-9197-4c2b-9a58-709dbf338f78",
                "hash": "593349467a7dd7aa418099dc2925fcba732fbc8c45e051638b95a752d8522387"
            }
        },
        {
            "id": "74b7c148-dabe-408d-a443-31562b10a80a",
            "status": "pending", //1st persisted status of wallet
            "createdAt": "2021-03-24T13:15:02.121Z",
            "updatedAt": "2021-03-24T13:15:02.121Z",
            "additionalData": {}
        }
    ],
    "stellar": {
        "publicKey": "GDDVHXQRY2W35TTRXLKUTPMZCP3OZTN6OCZLN4F2KYTZLZEBDQXDYP4R" //blochchain hash registration
    },
    "updatedAt": "2021-03-24T13:15:02.112Z",
    "createdAt": "2021-03-24T13:15:02.112Z",
    "deletedAt": null,
    "user": {
        "id": "119fc608-64f6-4f83-8344-5c322b35d910",
        "name": "Name of Consumer", //consumer owner of wallet
        "firstName": "Name of Consumer",
        "lastName": "lastname od Consumer",
        "username": "consumer@email.com", 
        "email": "consumer@email.com",
        "role": "consumer", // role
        "twoFactorRequired": false, // two factor not active in this consumer
        "updatedAt": "2021-03-24T13:15:01.973Z",
        "createdAt": "2021-03-24T13:15:01.973Z",
        "domain": {
            "id": "c0346fb6-f606-480e-bf65-8d77d0730d60", //domainID of consumer
            "name": "trinus tech", // domain of consumer
            "role": "common"
        }
    },
    "additionalData": {
        "acceptProviderLegalTerms": true,
        "fingerprint": "PostmanRuntime/7.26.8#189.120.78.15" //fingertip of where consumer has acceptep the legal terms to use the plaftorm
    },
    "assets": [ // list of all asset in thie wallet
        {
            "pendingBalance": {
                "amount": "13.0000000" // if some transfers still not "settled" it will show as "pendingBalance"
            },
            "balance": "87.0000000",
            "authorizableBalance": "87.0000000", //THE REAL AMOUNT AVALIABLE here is where must be show to consumer front
            "consolidatedBalance": "100.0000000",
            "provider": "parati-provider", //provider of this asset
            "code": "BRLP", //accet code
            "name": "BRL Parati", //asset name
            "deletedAt": null,
            "updatedAt": {},
            "createdAt": {},
            "id": "c4b54553-935b-461c-b5e0-6dbc8a39b72b" // assetID
        },
        {
            "pendingBalance": {
                "amount": "0.0000000" // if some transfers still not "settled" it will show as "pendingBalance"
            },
            "balance": "0.0000000",
            "authorizableBalance": "0.0000000", //THE REAL AMOUNT AVALIABLE here is where must be show to consumer front (if necessary)
            "consolidatedBalance": "0.0000000",
            "provider": "bs2", //provider of this asset
            "code": "BRLB", //asset code
            "name": "BRL BS2", //asset name
            "deletedAt": null,
            "updatedAt": {},
            "createdAt": {},
            "id": "06099790-f403-41ce-8882-38ceb2865d68" //assetID
        },
        {
            "pendingBalance": {
                "amount": "0.0000000"
            },
            "balance": "0.0000000",
            "authorizableBalance": "0.0000000",
            "consolidatedBalance": "0.0000000",
            "provider": "celcoin-provider",
            "code": "BRLN",
            "name": "BRL Celcoin",
            "deletedAt": null,
            "updatedAt": {},
            "createdAt": {},
            "id": "f046702e-f76f-4f03-9686-2975748a3a71"
        }
    ]
}
```


<br />

### **Schema Response for `GET {{API_BASE_URL}}/wallets/:id` in Core v3**


```
{
    "id": "c2f15407-a567-4795-9f4d-a4dffcc40ae6",
    "status": "ready",
    "states": [
        {
            "id": "712fe93f-aabe-48f7-858d-4dfe4068044e",
            "status": "registered",
            "createdAt": "2021-03-17T15:27:17.217Z",
            "updatedAt": "2021-03-17T15:27:17.217Z",
            "additionalData": {
                "transaction": "ea278329-1a5a-454f-a898-54b079a3e0b8",
                "hash": "fab7e0a36eb0ef5b4c27b4eb2897eb57225916c4a56e4718a1fb08982dd73455"
            }
        },
        {
            "id": "92d488c8-3455-45de-90aa-1b87485e7ed9",
            "status": "pending",
            "createdAt": "2021-03-17T15:27:13.517Z",
            "updatedAt": "2021-03-17T15:27:13.517Z",
            "additionalData": {}
        }
    ],
    "stellar": {
        "publicKey": "GA7S2HWITAOMQORM6KOWFZTBZ3GSVF5ZFRNDHYJJBP7XXM54GHSCJP63"
    },
    "updatedAt": "2021-03-17T15:27:13.498Z",
    "createdAt": "2021-03-17T15:27:13.498Z",
    "deletedAt": null,
    "user": {
        "id": "31224b73-5b26-4cac-b74e-e30ef1f99384",
        "name": "Brunao Vieira",
        "firstName": "Brunao",
        "lastName": "Vieira",
        "username": "brunovieria231@email.com",
        "email": "a_semana_inteir@fiqueitees.pe",
        "role": "consumer",
        "twoFactorRequired": false,
        "updatedAt": "2021-03-19T17:58:03.963Z",
        "createdAt": "2021-03-17T15:27:13.298Z",
        "domain": {
            "id": "7f717a62-a2d2-4fec-a8aa-ce2b2dbbdf4e",
            "name": "NOSSO DOMINIO",
            "role": "common"
        }
    },
    "additionalData": {
        "acceptProviderLegalTerms": true,
        "fingerprint": "PostmanRuntime/7.26.10#35.237.4.70"
    },
    "assets": [
        {
            "pendingBalance": {
                "amount": "0.0000000"
            },
            "balance": "89.0000000",
            "authorizableBalance": "89.0000000",
            "consolidatedBalance": "89.0000000",
            "provider": "parati-provider",
            "code": "BRLP",
            "name": "BRL Parati",
            "deletedAt": null,
            "updatedAt": {},
            "createdAt": {},
            "id": "33b986c9-23ee-4262-ada7-0c9ed1b07b66"
        },
        {
            "pendingBalance": {
                "amount": "0.0000000"
            },
            "balance": "0.0000000",
            "authorizableBalance": "0.0000000",
            "consolidatedBalance": "0.0000000",
            "provider": null,
            "code": "TCN",
            "name": "Test Coin",
            "deletedAt": null,
            "updatedAt": {},
            "createdAt": {},
            "id": "150e9076-72cb-43b5-a3db-956f7584c422"
        },
        {
            "pendingBalance": {
                "amount": "0.0000000"
            },
            "balance": "0.0000000",
            "authorizableBalance": "0.0000000",
            "consolidatedBalance": "0.0000000",
            "provider": "bs2",
            "code": "BRLB",
            "name": "BRL Bs2",
            "deletedAt": null,
            "updatedAt": {},
            "createdAt": {},
            "id": "63f4af75-8bfb-4925-ade0-265337770297"
        }
    ]
}
```
 
<br />


### **Schema response for payment `BOLETO-IN`**

```
    {
        "banking": null, // not aplicable in boleto_in type payment 
        "payments": [
            {
                "status": "settled", // final sattus of a PAYMENT
                "type": "boleto_in", // type of payment
                "destination": {
                    "id": "80349602-ad67-4737-a06b-e9918b51a38e", // the walletID of destination consumer
                    "stellar": {
                        "publicKey": "GBIMVYYXYLNZ5ZW5WVL36MHG2G26VPOBEQ5KDGIMCDGXOKFRCBSSDUTZ" // blockchain register of this transaction
                    },
                    "updatedAt": "2020-09-16T19:38:59.663Z",
                    "createdAt": "2020-09-16T19:38:59.663Z",
                    "deletedAt": null,
                    "user": {
                        "id": "c07bd96c-59aa-4677-8bb6-9765a83f205d", //userID consumer destination
                        "name": "Bruno da Silva Vieira", //name ofd estination consumer
                        "firstName": "Bruno da Silva",
                        "lastName": "Vieira",
                        "email": "bruno.vieira@outlook.com",
                        "role": "consumer",
                        "twoFactorRequired": false,
                        "updatedAt": "2021-03-26T17:24:36.576Z",
                        "createdAt": "2020-09-16T19:38:58.753Z"
                    },
                    "additionalData": {}
                },
                "amount": "5.01", // tha amount of payment
                "asset": {
                    "id": "98a4e3eb-cfef-4f64-b7c8-fcfe29e6378f",
                    "name": "BRL BS2", // name of asset of this payment
                    "code": "BRLB", // asset code of this paymen
                    "root": false, // not root asset
                    "provider": "bs2", // provider of asset
                    "required": false, //not required asset 
                    "updatedAt": "2020-08-05T23:53:47.775Z",
                    "createdAt": "2020-08-05T23:53:47.775Z"
                },
                "scheduleFor": null, // not aplicable in boleto_in type payment 
                "updatedAt": "2021-02-18T10:25:45.554Z",
                "createdAt": "2021-02-18T10:25:45.554Z",
                "id": "aca994b4-ad3e-4819-b0b5-4106376d5eb9" // paymentID of destination side of transaction
            }
        ],
        "source": {
            "id": "106d6869-d475-4e38-b586-905acd80a720", //walletID of source of payment
            "root": true,
            "stellar": {
                "publicKey": "GAGPSIHDVEMMMH55GI3YNNR4KPU4OKZGF3XBOWYRCJWCNZNT4PHVI2DC" // registration of this wallet in blockchain
            },
            "updatedAt": "2020-05-05T20:18:03.421Z",
            "createdAt": "2020-05-05T20:18:03.421Z",
            "deletedAt": null,
            "user": {
                "id": "64698d90-cf84-466a-99a6-63b6214878e9", //walletID of the source
                "name": "Bit Capital Issuer", // name of the source of payment ( If Bit Capital Issuer, this means is external income amount,)
                "firstName": "Bit Capital",
                "lastName": "Issuer",
                "email": "admin@btcore.app",
                "role": "admin",
                "twoFactorRequired": false,
                "updatedAt": "2020-05-05T20:18:03.397Z",
                "createdAt": "2020-05-05T20:18:03.397Z"
            },
            "additionalData": {}
        },
        "states": [
            {
                "additionalData": {
                    "pod": "production-core-core-api-transaction-workers-997556467-59fqn"
                },
                "updatedAt": "2021-02-18T10:25:52.451Z",
                "createdAt": "2021-02-18T10:25:52.451Z",
                "status": "notified", // last state of a transaction ( 5th)
                "id": "c85fb1c4-7d29-4fc4-8e71-581d99e61614"
            },
            {
                "additionalData": {
                    "pod": "production-core-core-api-transaction-workers-997556467-lhlz8"
                },
                "updatedAt": "2021-02-18T10:25:51.860Z",
                "createdAt": "2021-02-18T10:25:51.860Z",
                "status": "executed", // 4th state of a transaction
                "id": "dc5aab34-d4ea-40c9-af89-27a31c6b37ce"
            },
            {
                "additionalData": {
                    "authorized": [],
                    "pod": "production-core-core-api-server-7fcb6dc58b-qwf8h"
                },
                "updatedAt": "2021-02-18T10:25:47.124Z",
                "createdAt": "2021-02-18T10:25:45.596Z",
                "status": "accepted", // 3rd state of a transaction
                "id": "5052a5bd-2971-42a7-997e-b327cfe59892"
            },
            {
                "additionalData": {
                    "authorized": [],
                    "skipped": [
                        {
                            "provider": "bs2",
                            "payment": "aca994b4-ad3e-4819-b0b5-4106376d5eb9",
                            "asset": "BRLB" // the asset of transaction
                        }
                    ]
                },
                "updatedAt": "2021-02-18T10:25:45.580Z",
                "createdAt": "2021-02-18T10:25:45.580Z",
                "status": "AUTHORIZED", // 2nd state of a transaction ( here the transaction is registered in blockchain
                "id": "86e38300-5a59-4bb5-80f0-8881b408a370"
            },
            {
                "additionalData": {},
                "updatedAt": "2021-02-18T10:25:45.546Z",
                "createdAt": "2021-02-18T10:25:45.546Z",
                "status": "pending", // 1st state of a transaction
                "id": "1df95a55-1803-43de-91b6-ca283dae2928"
            }
        ],
        "updatedAt": "2021-02-18T10:25:51.073Z",
        "createdAt": "2021-02-18T10:25:45.540Z",
        "additionalData": {
            "externalTransaction": { // here we can identify which boleto is referred
                "postbackId": "9863f8e4-525e-49a2-aa1e-442dd7c633fd",
                "createdAt": "2021-02-18T07:25:42.4938016-03:00", //
                "id": "c1d8b05c-01b0-4362-a860-7a7500a8b207" // this id is the boletoID already paid, with this id you can identify what Boleto it refers,is very important this infomation. To see tha datas of boleto you need to use the endpoint GET {{API_BASE_URL}}/boletos/{{boletoID}}.  
            },
            "hash": "e6264f8b9d5aff8bf1f90367448d8d22628d30f19cffee6aebe8f7cb4e846649"
        },
        "status": "notified", //status of this transaction
        "type": "payment", // type of this transaction
        "id": "279a4791-1b16-4224-8f23-39987524526f" // the transactionID 
    }
```

<br />

### **Schema response for payment TED-OUT `POST {{API_BASE_URL}}/wallets/:id/withdraw`**

```
{
    "banking": { //information about the favoured person registered in platform. See Favoured management in TED-OUT section
        "accountDigit": "",
        "account": "9180733", 
        "agencyDigit": "0",
        "agency": "1", 
        "bank": "260", //bank number (COMPE)
        "type": "checking", 
        "holderType": "personal", //personal or corporate
        "taxId": "32322929840", //CNPJ or CNPJ
        "name": "Name of Consumer Destination",
        "updatedAt": "2021-03-15T17:57:47.347Z",
        "createdAt": "2021-03-15T17:57:47.347Z",
        "id": "28af131f-65d2-463c-bda3-006e30a53b54" //the bankingID of favoured person
    },
    "payments": [
        {
            "status": "settled", //the last state of a payment
            "type": "withdrawal", // money movement of trasnaction ( see Finance Management section)
            "destination": { // all informations about the destination starts here
                "id": "98f2a79e-fcfe-4d16-bc29-1afb8dcd1f17",
                "root": true,
                "stellar": {
                    "publicKey": "GAGPSIHDVEMMMH55GI3YNNR4KPU4OKZGF3XBOWYRCJWCNZNT4PHVI2DC" /blockchain registerof this wallet
                },
                "updatedAt": "2021-02-16T01:45:51.520Z",
                "createdAt": "2021-02-16T01:45:51.520Z",
                "deletedAt": null,
                "user": {
                    "id": "c3df1c5e-51fa-49e8-8d0d-4e185d1b029b", //userID of destination
                    "name": "Bit Capital Issuer", /name of consumer of destination **IMPORTANT: TO UNDERSTAND WHAT MEANS BIT CAPITAL ISSUER PLEASE VISIT "FINANCE MANAGEMENT SECTION"
                    "firstName": "Bit Capital",
                    "lastName": "Issuer",
                    "username": "admin@btcore.app",
                    "email": "admin@btcore.app",
                    "role": "admin",
                    "twoFactorRequired": false,
                    "updatedAt": "2021-02-16T01:45:51.586Z",
                    "createdAt": "2021-02-16T01:45:51.494Z"
                },
                "additionalData": {}  //some additional info about this wallet
            },
            "amount": "9.00", //the amount of this payment
            "asset": { //some infomations about the asset of this payment
                "id": "1a7f988b-5c7b-4549-93c2-a0fe509dfa4a", //payment's assetID 
                "name": "BRL Parati",
                "code": "BRLP", //payment's asset code
                "root": true,
                "provider": "parati-provider",
                "required": true,
                "updatedAt": "2021-02-16T01:45:51.529Z",
                "createdAt": "2021-02-16T01:45:51.529Z"
            },
            "scheduleFor": null, //if a scheduled TED, this filed must be filled
            "updatedAt": "2021-03-15T18:23:27.760Z",
            "createdAt": "2021-03-15T17:57:47.679Z",
            "id": "69c009c4-f637-4f3d-b67a-a3c94c89771e"  //the paymentID of this payment
        }
    ],
    "source": { //all information about the source starts here
        "id": "41048161-05a9-4411-b033-cff78d1018b4", //walletID of consumer of source
        "stellar": {
            "publicKey": "GB3UXUGZWEQEWWLDIESBOKUMM5EVK3Z3EMLFKI2YLBOF4L5264JB2HOL"  //blockchain register of this wallet
        },
        "updatedAt": "2021-02-25T17:14:55.742Z",
        "createdAt": "2021-02-25T17:14:55.742Z",
        "deletedAt": null,
        "user": {
            "id": "bd40d656-bd7b-46ed-8362-fc0296d5330b", //userID of consumer of source
            "name": "Name of Consumer Source", //name of consumer of source 
            "firstName": "Name of Consumer",
            "lastName": "Source",
            "username": "userNameConsumer",
            "email": "userName@email.com",
            "role": "consumer",
            "twoFactorRequired": false,
            "updatedAt": "2021-02-25T17:14:55.564Z",
            "createdAt": "2021-02-25T17:14:55.564Z"
        }, 
        "additionalData": { //some additional info about this wallet
            "acceptProviderLegalTerms": true,
            "fingerprint": "PostmanRuntime/7.26.10#179.113.244.183"  //the fingertip of legal terms acceptance
        }
    },
    "states": [ //here starts all informations about the status os this transaction, the timeline of payments
        {
            "additionalData": {
                "pod": "production-core-core-api-transaction-workers-6b6676f989-ds69q"
            },
            "updatedAt": "2021-03-15T18:23:35.074Z",
            "createdAt": "2021-03-15T18:23:35.074Z",
            "status": "notified", // the last state of a transaction. It means all done, and all webhooks sent.
            "id": "878bfba3-830f-4f14-be69-8f00bf6bc438"
        },
        {
            "additionalData": {
                "pod": "production-core-core-api-transaction-workers-6b6676f989-dx564"
            },
            "updatedAt": "2021-03-15T18:23:34.423Z",
            "createdAt": "2021-03-15T18:23:34.423Z",
            "status": "executed", //the 4th state of a transaction. It means all done, but NOT sent webhook yet.
            "id": "89cde4ab-f58b-493a-b5f0-a0ab1abd84b8"
        },
        {
            "additionalData": {
                "authorized": [],
                "pod": "production-core-core-api-server-6449f74964-m5frz"
            },
            "updatedAt": "2021-03-15T18:23:30.761Z",
            "createdAt": "2021-03-15T18:23:27.783Z",
            "status": "accepted",  // 3rd state of a transaction. A necessary state to measure our SLA in BACEN. It means both sides accepted the transaction and we sent a notification to BACEN
            "id": "ad602168-33cf-4d35-af26-76f8523d14de"
        },
        {
            "additionalData": { //some additional necessary infos
                "authorized": [],
                "skipped": [
                    {
                        "provider": "parati-provider", // the provider of the asset
                        "payment": "69c009c4-f637-4f3d-b67a-a3c94c89771e", // the paymentID (again)
                        "asset": "BRLP"  // the asset of the AUTHORIZED state
                    }
                ]
            },
            "updatedAt": "2021-03-15T17:57:47.704Z",
            "createdAt": "2021-03-15T17:57:47.704Z",
            "status": "AUTHORIZED", // the 2nd state of payment. It means this transaction is written in blockchain. At this point is not possible to cancel this transaction. If a destination consumer was not found, or some data errors was typed, after this transaction was TOTALLY COMPLETED, a new transactionn will be created with the type "transaction_reversal" to credit all values to teh source. 
            "id": "e0dccc7b-1c5d-4ced-8a4a-42a469f81162"
        },
        {
            "additionalData": {},
            "updatedAt": "2021-03-15T17:57:47.673Z",
            "createdAt": "2021-03-15T17:57:47.673Z",
            "status": "pending", //the first state of a transaction. Where the transaction starts.
            "id": "beb06977-2238-479c-9e32-5760ef12e7a3"
        }
    ],
    "updatedAt": "2021-03-15T18:23:33.997Z",
    "createdAt": "2021-03-15T17:57:47.667Z",
    "additionalData": { //this additionalData show all data received by BACEN
        "transactionId": "jaYMBH3qms",
        "referenceCode": "jaYMBH3qms",
        "destination": {
            "accountHolderTaxId": "32322929840",
            "accountHolderType": "personal",
            "accountHolderName": "Name of Consumer Destination",
            "accountNumber": "9180733",
            "branchNumber": "1",
            "accountType": "checking",
            "bankNumber": "260",
            "ispb": "18236120"
        },
        "arrangement": "str",  //if TED is "str" if PIX is "pix"
        "reversal": false,
        "purpose": 10, //BACEN purpose
        "source": {
            "accountHolderTaxId": "32322929840",
            "accountHolderType": "personal",
            "accountHolderName": "Name of Consumer Source",
            "accountNumber": "10905",
            "branchNumber": "0001",
            "accountType": "checking",
            "bankNumber": "326",
            "ispb": "3311443"
        },
        "hash": "e365737d2811787e0f5f4421713feea1655f29bba8e1ebf49b8672ec54d8ee76",
        "str": {
            "messageCode": "STR0008R1",  //STR message Code. To get all possible messages from STR, download in https://www.bcb.gov.br/content/estabilidadefinanceira/cedsfn/Catalogos/Catalogo_de_Servicos_do_SFN_Volume_I_Versao_502.pdf
            "messageId": "STR20210315035110883" //STR message
        }
    },
    "status": "notified",  //the last status of transaction
    "type": "payment", //type of transaction
    "id": "c40a36c3-bd73-4a1a-9bd2-f21c84414b36" //transactionID
}
```
<br />

### **Schema response for payment `TED-IN`**

```
{
    "banking": null, //if the payment has a favoured, all information will be displayed here
    "payments": [
        {
            "status": "settled", //the last state of a payment
            "type": "deposit", // money movement of trasnaction ( see Finance Management section)
            "destination": { // all informations about the destination starts here
                "id": "feb8503c-d7aa-4f85-8333-6a705f95b533", //walletID of consumer of destination
                "stellar": {
                    "publicKey": "GDNFHUD5ZCFW4MMHHQ2GDXWFRLQAMYQMJLCTKVBGNEZYXYPFPSJTNJZO" //blockchain registerof this wallet
                },
                "updatedAt": "2021-03-19T13:13:45.065Z",
                "createdAt": "2021-03-19T13:13:45.065Z",
                "deletedAt": null,
                "user": { 
                    "id": "01261a24-9a73-4360-b2b8-d04a483571f5", //userID of destination
                    "name": "Consumer of Destination", //name of consumer of destination
                    "firstName": "Consumer", 
                    "lastName": "of Destination",
                    "username": "userNameOfCOnsumer",
                    "email": "emailconsumerdestination@email.com", //email of consumer of destination
                    "role": "consumer",
                    "twoFactorRequired": false,
                    "updatedAt": "2021-03-19T13:13:44.809Z",
                    "createdAt": "2021-03-19T13:13:44.809Z"
                },
                "additionalData": { //some additional info about this wallet
                    "acceptProviderLegalTerms": true,
                    "fingerprint": "PostmanRuntime/7.26.10#187.34.144.47" //the fingertip of legal terms acceptance
                }
            },
            "amount": "1.00", //the amount of this payment
            "asset": { //some infomations about the asset of this payment
                "id": "c4b54553-935b-461c-b5e0-6dbc8a39b72b", //payment's assetID 
                "name": "BRL Parati",
                "code": "BRLP", //payment's asset code
                "root": true, 
                "provider": "parati-provider",
                "required": true,
                "updatedAt": "2021-03-11T01:30:37.900Z",
                "createdAt": "2021-03-11T01:30:37.900Z"
            },
            "scheduleFor": null, //if a scheduled TED, this filed must be filled
            "updatedAt": "2021-03-19T18:50:43.656Z",
            "createdAt": "2021-03-19T18:50:43.656Z",
            "id": "48da5e61-3b71-49b7-bebe-3566c492ecfa" //the paymentID of this payment
        }
    ],
    "source": { //all information about the source starts here
        "id": "6010622e-0c63-4082-a8a2-8da98fcb7787", //walletID of consumer of source
        "root": true, 
        "stellar": {
            "publicKey": "GAGPSIHDVEMMMH55GI3YNNR4KPU4OKZGF3XBOWYRCJWCNZNT4PHVI2DC" //blockchain register of this wallet
        },
        "updatedAt": "2021-03-11T01:30:37.884Z",
        "createdAt": "2021-03-11T01:30:37.884Z",
        "deletedAt": null,
        "user": { 
            "id": "cbb474f7-6eb2-433b-b655-936bf2645ffe", //userID of consumer of source
            "name": "Bit Capital Issuer", //name of consumer of source **IMPORTANT: TO UNDERSTAND WHAT MEANS BIT CAPITAL ISSUER PLEASE VISIT "FINANCE MANAGEMENT SECTION"
            "firstName": "Bit Capital",
            "lastName": "Issuer",
            "username": "admin@btcore.app",
            "email": "admin@btcore.app",
            "role": "admin",
            "twoFactorRequired": false,
            "updatedAt": "2021-03-11T01:30:38.106Z",
            "createdAt": "2021-03-11T01:30:37.849Z"
        },
        "additionalData": {} //some additional info about this wallet
    },
    "states": [ //here starts all informations about the status os this transaction, the timeline of payments
        {
            "additionalData": {
                "pod": "production-core-core-api-transaction-workers-57d9d58f65-wg9xh"
            },
            "updatedAt": "2021-03-19T18:50:51.702Z",
            "createdAt": "2021-03-19T18:50:51.702Z",
            "status": "notified",  // the last state of a transaction. It means all done, and all webhooks sent.
            "id": "4cc0c34b-0218-4030-826c-93cbb7b2a77a"
        },
        {
            "additionalData": {
                "pod": "production-core-core-api-transaction-workers-57d9d58f65-frwbx"
            },
            "updatedAt": "2021-03-19T18:50:50.646Z",
            "createdAt": "2021-03-19T18:50:50.646Z",
            "status": "executed", //the 4th state of a transaction. It means all done, but NOT sent webhook yet.
            "id": "a1770070-3dbb-4022-8803-d795c123070c"
        },
        {
            "additionalData": {
                "authorized": [],
                "pod": "production-core-core-api-server-5994b5d7cd-fszzr"
            },
            "updatedAt": "2021-03-19T18:50:47.006Z",
            "createdAt": "2021-03-19T18:50:44.047Z",
            "status": "accepted", // 3rd state of a transaction. A necessary state to measure our SLA in BACEN. It means both sides accepted the transaction and we sent a notification to BACEN
            "id": "ff8073f1-2f4e-4b69-9e14-dbf28287b1cb"
        },
        {
            "additionalData": { //some additional necessary infos
                "authorized": [],
                "skipped": [
                    {
                        "provider": "parati-provider", // the provider of the asset
                        "payment": "48da5e61-3b71-49b7-bebe-3566c492ecfa", // the paymentID (again)
                        "asset": "BRLP" // the asset of the AUTHORIZED state
                    }
                ]
            },
            "updatedAt": "2021-03-19T18:50:43.692Z",
            "createdAt": "2021-03-19T18:50:43.692Z",
            "status": "AUTHORIZED", // the 2nd state of payment. It means this transaction is written in blockchain. At this point is not possible to cancel this transaction. If a destination consumer was not found, or some data errors was typed, after this transaction was TOTALLY COMPLETED, a new transactionn will be created with the type "transaction_reversal" to credit all values to teh source. 
            "id": "cb260d9b-cc79-4eca-9eaa-5c9e5b4ab63c"
        },
        {
            "additionalData": {},
            "updatedAt": "2021-03-19T18:50:43.589Z",
            "createdAt": "2021-03-19T18:50:43.589Z",
            "status": "pending", //the first state of a transaction. Where the transaction starts.
            "id": "55bff677-12b2-480c-939f-5daf6d1d04ef"
        }
    ],
    "updatedAt": "2021-03-19T18:50:50.032Z", 
    "createdAt": "2021-03-19T18:50:43.574Z", 
    "additionalData": { //this additionalData show all data received by BACEN
        "externalTransaction": {
            "id": "STR20210319034211531" //the STR message
        },
        "destination": { //data of destination
            "accountHolderTaxId": "32322929840",
            "accountHolderType": "personal",
            "accountHolderName": "NAME OF CONSUMER DESTINATION",
            "accountNumber": "17004",
            "branchNumber": "1",
            "accountType": "checking",
            "bankNumber": "326",
            "ispb": "03311443"
        },
        "arrangement": "str", //if TED is "str" if PIX is "pix"
        "reversal": false,
        "purpose": "Crédito em Conta", //BACEN purpose
        "source": {
            "accountHolderTaxId": "32322929840",
            "accountHolderType": "personal",
            "accountHolderName": "NAME OF CONSUMER SOURCE",
            "accountNumber": "9180733",
            "branchNumber": "1",
            "accountType": "checking",
            "bankNumber": "260",
            "ispb": "18236120"
        },
        "hash": "e086a38506350fb32362c86a33db3019599a6ae30f0b726d3523e52d5ec9e05f",
        "str": {
            "messageCode": "STR0008R2", //STR message Code. To get all possible messages from STR, download in https://www.bcb.gov.br/content/estabilidadefinanceira/cedsfn/Catalogos/Catalogo_de_Servicos_do_SFN_Volume_I_Versao_502.pdf
            "messageId": "STR20210319034211531" //STR message
        }
    },
    "status": "notified", //the last status of transaction
    "type": "payment", //type of transaction
    "id": "c3a75969-aec0-4a10-a038-6cfa2f445cc6" //transactionID
}

```

<br />



# 5 - Labs Bit Capital

You can check tools for help here [Labs Bit Capital](https://labs.btcore.app) in the Bitcapital Labs for more information and sample codes.

<br />

----
# 6 - Glossary

| term | where to find | info |
| --- | --- | --- |
| `partner` | TBA | the corporation contractor of Bit Capital Services. This partner has a `mediator` login |
| `mediator` | TBA | a login to access Bit Capital's platform by the Partner |
| `consumer` | TBA | a costumer of partner. To distinguish our partner to a consumer in the end of chain.  |
| `asset` | TBA | the money representation in platform. |
| `BRLP` | TBA | the asset code representation of Brazilian Real in the platfom |
| `domain` | TBA | part of infrastructure delivered to our partner to and register the consumers of yours  |
| `instance` | [Understanding your platfom](https://docs.bitcapital.com.br/?version=latest#understanding-your-platform) | the infrastructure environment delivered to our partners  |
| `payment` | [Payments](https://docs.bitcapital.com.br/?version=latest#6febc303-f8a3-4cc5-bfd1-b172e52557a9) | all kind of payment in the platform |
| `transaction` | [Finance management](https://docs.bitcapital.com.br/?version=latest#c23dea8a-d7a8-4091-9fdd-f8889268a534) | represents changes in blockchain |
| `mediator` | [Introduction](https://docs.bitcapital.com.br/?version=latest#intro) | maximum permission of a partner |
| `onboarding` | [Onboarding](https://docs.bitcapital.com.br/?version=latest#a8cada24-8c2f-440a-a11a-05d5136cd11a) | al |
| `ispb` | true | identification of Finance Insitution in BACEN ( identificação no Sitema de Pagamentos Brasileiro |
| `platform` | TBA | all environment and API avaliable to our partner |
| `actor` | TBA | the human person that executes a endpoint |
| `blockchain` | TBA | ledger where all transactions are registered |
| `stellar` | TBA | the technology used in our Blockchain |
| `BACEN` | TBA | central bank of Brazil |
| `SPI` | TBA | Instant Payment System (Sistema de Pagamentos Instantâneos) used um PIX API |
| `SPB` | TBA | Brazilian system payment (Sistema de Pagamentos Brasileiro) used in Core AP |
| `no-named card` | [Cards](https://docs.bitcapital.com.br/?version=latest#651b95ad-2d3e-4cc0-84cc-070883d0a241) | physical cards embossed with no name. |

----
# 7 - Documentation CHANGELOG 


Some endpoints become obsolete for use and others will be accredited. Below are all the updates of the Documentation and Endpoints.

```
#### Documentation v3.0.50

- [x] added new endpoints:
-- Onboarding / Core 3.x.x / Corporate

#### Documentation v3.0.13

- [x] Deprecated endpoint information:
-- Cards / Card payments

- [x] added new endpoints: 
-- Cards / unblock no-named card
-- Environment management / Edit webhook URL

- [x] added TED-IN and TED-OUT Schema in Schema response section;
- [x] added STR messages code in Finance management section;

#### Documentation v3.0.10
- [x] added new section SDK Development;
- [x] added new section Schema Response;
- [x] added new endpoints: 
-- Finance management / Judicials / Blocking partial or total balance
-- Boleto / Boleto Pay / Payment proof 

#### Documentation v3.0.7
- [x] added new endpoints: 
-- Finance management / Create a new wallet
-- Finance management / Payment statement by asset
- [x] added Glossary section;
- [x] added more documentation about Cards;
- [x] started documentation of PIX API; 

#### Documentation v3.0.7
- [x] added documentations about Cards
- [x] added UML graphics in sections: Boleto, Finance management ans P2P

#### Documentation v3.0.5
- [x] added new endpoint:
-- TED / TED OUT scheduled;
- [x] added documentation about Money Movement in Finance management section

#### Documentation v3.0.4
- [x] added documentation of TED-IN and TED-OUT in TED section;
- [x] added documentation section for "Assets management" in:
-- Finance management / Assets management 


#### Documentation v3.0.3
- [x] added documentation of status in Onboarding section;
- [x] added some payload examples of received TED-IN and received BOLETO;

#### Documentation v3.0.1
- [x] added new endpoints: 
-- User management / Administrative users / Create administrative users

#### Documentation v3
- [x] equalized the Documentation version (this site) to the API version. Now the documentations will follow the laytest version of API avaliable.

#### Documentation v2.4.2
- [x] added new endpoints: 
-- Boleto / Boleto Pay / Payment proof
-- Boleto /Boleto Emit / Emit a Boleto to a payer
-- Billing management / Plans / Create a plan with absolute fees
-- Billing management / Plans / Create a plan with % fees

- [x] added new informatiosn about Billing in Billing section

#### Documentation v2.4.1
- [x] added full information about Billing Management and it's dependencies
- [x] added link to Labs Bit Capital. Tools for troubleshooting some codes

#### Documentation v2.4
- [x] rearranged the endpoint structure of Onboarding section. Now it is possible to follow the necessary steps according to your version of the instance;
- [x] added endpoint GET /accounting/wallet-balance in "Accounting" section;

#### Documentation v2.3
- [x] New endpoints for * Onboarding * to meet version 3.0 of the **Bitcapital Core API**;
- [x] Legacy Onboarding endpoints are rearranged in the "deprecated" folder within Onboarding;
```

<br />

----

<br />

----

<br />