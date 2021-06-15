Welcome to moonbeam!  cloudwi.re is pleased to present our short code SMS API to the masses.  Our job is to keep you compliant, provide a high degree of message deliverability, provide rocket throttle and crush your long code filtering woes.  

We're a happy bunch here.  We want to make you a happy developer.  You'll find that some of our documentation can be redundant.  It is designed that way to make life a bit easier when learning concepts and hopefully prevent you from having to re-review to find something.  Let's get started.  

## Compliance
The cloudwi.re SMS API is built for compliance in line with the Mobile Marketing Association guide to best practices, which meets the TCPA guidelines set forth by the FCC.  cloudwi.re handles the opt-in logic and the developer can focus on sending/receiving messages without worry.  By our Terms & Conditions, you must also be responsible for compliance.  So don't send opt-in requests or confirmations to subscribers who haven't granted you consent.  

NO, you cannot send opt-in requests to subscribers blindly just because you have a business relationship with them.  You must have consent.

## Proud Twilio Partner
It's a 9 out of 10 chance you are here because someone @Twilio referred you to us.  In turn, we are here because of Twilio.  The Twilio-cloudwi.re partnership is nearly eight years old and those benefits are extended to the developer by way of a fully featured shared short code platform.  cloudwi.re is a Premier Twilio partner.

## Subscriber Experience
cloudwire is built for speed as much for the developer as it is for the subscriber.  cloudwi.re generally processes an inbound keyword and returns the proper template to our aggregator for delivery in an average of 1 tenth of a second.  All in a process that requires searching over 20k accounts and 40M subscriber records.  

Additionally, cloudwire breaks down campaigns into a separate bucket so as not to eat away at short code bandwidth and create unnecessary message latency for someone simply trying to get a coupon.  

The result is a happier subscriber with snappy responses to their inquiries.

## Read the Docs and Guides!
We get it.  It's a long read and nobody likes to read! But the documentation is detailed to help you.  It is rare that you will need us to answer any questions.  But we are here if you do need us.  Support is always free and responsive.  But please keep it that way by exploring the documentation first! 

Keep in mind when reading that some use cases are not supported by the published API.  These features are hidden for compliance reasons.  Don't hesitate to contact us if that means you.  We can just about handle any use case. 

And please forgive our redundancy in some sections.  We do this only to reinforce learning the platform.

## Getting Support
We are easily accessible at <a href="mailto:support@cloudwi.re">support@cloudwi.re</a> free of charge.  But PLEASE......help us help you.  We cannot solve problems when you tell us you didn't get a text.  If you are having trouble connecting to the API make sure you include your code.  Can't send a message?  We need your <i>accountId</i>, <i>mobileId</i> and the relative time the message was attempted.  The more data you can educate us with the better chance we can solve your problem in a timely manner.

## Platform Status
cloudwi.re maintains and reports errors from our status page for API, UI and carrier delivery issues.  Status updates are only sent to those signed up on the status page.  You can sign up <a href="http://at4armed.cloudwi.re">HERE.</a>

## Message Deliverability
cloudwi.re is built to give the developer the best chance of getting your message to the end user device.  If the subscriber carrier you are messaging isn't short code supported, we got you covered and we'll fire your message on a long code.  If the carrier is not MMS supported we'll fire a link to your image inside an SMS body.  And in some cases, if a fail or undelivered receipt is returned to us from the carrier we will fire the message on a long code.  Additionally, cloudwi.re is capable of 2-way messaging in many countries of the world using local long codes and sending 1-way outbound messaging to every country using global enabled USA long codes.  

## USA SMS/MMS
cloudwi.re is primarily built for USA short code messaging and supports 2-way SMS/MMS on most USA Carriers.  If a message is sent to a USA subscriber who is on a carrier that is not short code supported, the SMS API will send the message on a long code.  We support up to 1600 characters in a message but advise that you keep your character count to 160 or less.

USA Supported short code carriers can be found here <a href="https://cloudwire.gelato.io/guides/understanding-short-codes#us-short-codes-carrier-support" target="_blank">HERE.</a> Read on to learn about how the SMS API sends/receives SMS Canada and the rest of the world.

## Globally Agnostic
Although cloudwi.re is primarily built for USA short code messaging, the SMS API supports messaging to many countries.  It's important to note that international numbers cannot communicate with USA short codes.  This is especially important for anyone doing keyword campaigns.  The SMS API uses local and global enabled long codes to accomplish this.  

Further, the developer does not need to concern themselves with what countries their subscribers reside in or what numbers to utilize when transmitting SMS with them.  

We do that for you :)

## Communicating With The API
The cloudwi.re SMS API is tuned to consume your API messaging request and either successfully acknowledge receipt or error out based on certain conditions within the response synchronously. With regards to the messaging methods, it's important to note that a successful response from the SMS API does not indicate whether your message passed opt-in checks or was attempted or delivered.  It simply means we received it successfully and are processing your request.  You should prepare for both synchronous and asynchronous responses from the API.  

## Time Zones
The SMS API will deliver information to you in GMT only.  It is up to you to convert your time.  However, the store portal dashboards will convert your message logs into the selected store time zone. 

## Migrating an Opt-in List
cloudwi.re does not allow developers to upload opt-in data from a different vendor.  That task can be completed only by cloudwi.re team members.  Read up on list migrations if that means you. It will require you to fill out a cloudwi.re list migration form.  For more information on migration and to find the form, click <a href="https://cloudwire.gelato.io/guides/short-code-and-or-list-migration">here</a>.

cloudwi.re will load data for you unless this form is filled out for your account. It is not negotiable.  For more information, contact <a href="mailto:support@cloudwi.re?Subject=I%20Am%20Migrating%20From%20Another%20Vendor" target="_top">Support</a>.

## How You Are Billed for Messaging
For SMS, the carriers bill us in 160 character segments in most cases.  If you send an SMS that is 422 characters, it will be billed as 3 message segments.    Additionally, MMS is delivered as one payload by the carriers.  That means if you send an MMS, any SMS attached to that message is not included and you only pay the price of the MMS, regardless of the SMS character count.  

Any message that passes opt-in checks and is attempted for delivery is billable.

USA and Canadian SMS are priced the same.  

Additionally, some carriers charge extra jack to communicate with their subscribers on short codes.  This cost is included in cloudwi.re message pricing and there is no additional mark-up.

## Billing Portal
Billing is automated and outsourced by cloudwi.re.  It is separately hosted and the link to your account page can be accessed through the admin portal.  2-Factor authentication is required via email every 30 days in order to access your billing portal should you wish to review statements or change your billing information.  

Billing occurs on right around Net 30 of your subscription sign-up date.  Additionally, cloudwi.re runs billing scripts in the wee hours of the night daily.  Usage is not updated in real-time.

## Smart Encoding
In most cases, message segments are counted in 160 character increments.  However, certain characters must be converted to UCS2 encoding.  These are billed in 70 character segments.  Bear in mind that unless you are getting a little crazy with characters, this will not affect you except for emojis (See Below).

The SMS API will convert most UCS2 characters to GSM so there is nothing the developer needs to worry about.  Although we advise playing it safe and stick to sending GSM characters.  You can check encoding with this tool:

<a href="http://chadselph.github.io/smssplit/">SMS Encoding Check</a>

<a href="https://en.wikipedia.org/wiki/GSM_03.38#GSM_7_bit_default_alphabet_and_extension_table_of_3GPP_TS_23.038_.2F_GSM_03.38">GSM Characters Wiki</a>

## Emojis are encoded to UCS2!
The above is important to keep in mind when sending messages containing emojis 😬 👍 ❤️.  Any message with emojis will be encoded to UCS2 and bill in 70 character increments.  That greatly changes the amount of content you can fit into a message without being billed for 2 message segments.  Plan wisely.

Our take is that emojis do add a personal effect to the message and Clients that utilize them have reported higher response rates to their campaigns.

## How You Are Billed for Keywords
Keywords are added to your bill as soon as you reserve them.  They are pro-rated within your billing cycle.  If you sign-up for a keyword 15 days before your billing cycle is refreshed, you will only be charged for half the keyword fee.  

## Billing Methods
You can configure your billing preferences in the cloudwi.re admin portal.  cloudwi.re primarily accepts only USA/Canada addressed major credit cards.

# 2-Way Guaranteed SMS
Except where noted above with short code 345345, cloudwi.re guarantees 2-way SMS/MMS between opted-in subscribers and the store. There are no timing algorithms or sequences like our competitors utilize with only one short code. We achieve this by binding the opted-in subscriber to a short or long code to communicate with the store for the life of the opt-in.

The easiest way to understand this is to think of sending texts to your friends or significant other. All of them have unique phone numbers, right? Well, cloudwi.re kind of does the same thing.

We assign a unique short or long code for each subscriber to communicate with the store they are opted-in to for the life of the opt-in. The short code acts more like a proxy. But it's basically the same idea. That assignment, or bind, remains in place for the life of the opt-in. So, for example, if you opt-in to Jim's Pizza and you get a text from 24411 with your opt-in confirmation, you will always communicate with Jim's Pizza on 24411 while you are opted-in. But if you turn around and opt-in to Mercari, you'll be assigned a new short or long code to communicate with them and so on. 

What this does is allow cloudwi.re to determine, with 100% accuracy, that any inbound message after an opt-in event is routed to the correct store. So, if you text "I want a Pizza" to 24411, cloudwi.re knows that you are binded to Jim's Pizza on 24411 and we will pass the message on to the correct store. That happens even if the subscriber moved away for 4 years (while remaining opted-in) and then returned wanting your pizza.

## Building Keyword Decision Trees on Communication Codes (24411, 36546, 55398)
By way of the above, building keyword decision trees for subscribers binded to the communication short codes is rather easy.  cloudwi.re knows what subscriber is binded to what store via the communication short code proxy set up as the communication channel.  You can now ask for anything you want from the subscriber and cloudwi.re will post it to your webhook.  There are no timing algorithms or concerns for subscribers accidentally opt-in to other stores.  You can create a unique webhook for each store you create on cloudwi.re or you may use the same one.  We will post what store ID the subscriber is opted-in to when we receive the inbound message.  Then the developer can take whatever action that they choose.

The communication codes come into play whenever you call the API to opt-in a subscriber.  Additionally, subscribers are binded to the store via a communication short code when they utilize an opt-in keyword on the marketing code, 444999.  More on that as you read on.

## Building Keyword Decision Trees on Sticky Code (345345)
If you are going to opt-in subscribers via keyword and then put them into a decision tree, it's our recommendation that you do so with short code 444999 for reasons stated in <a href="https://cloudwire.gelato.io/docs/versions/moonbeam/the-cloudwi-re-short-code-concept">The cloudwe.re Short Code Concept</a>.  But sometimes that keyword you need might not be available and since you really want it, you book it on the sticky code (345345).  Since an opt-in keyword on 345345 will bind the subscriber for 2-way communications to 345345, there is the risk that a decision tree of back and forth messaging could result in the accidental opt-in of your subscriber to another cloudwi.re store.  

However, you can get around that with a little bit of creativity.  We recommend that you utilize a hash tag.  cloudwi.re does not allow special characters inside of a keyword.  That means that anyone that replies with a hash tag in front of what you are looking for is going to have their message posted to your store.  

You can collect birthdays, names and phone numbers.....or whatever.  Remember, in collecting email addresses, they have the @ symbol.  So you do not need to concern yourself with this since that symbol cannot be registered as a keyword.  

Fair warning though, if you are going to do natural language 2-way messaging with your opted-in subscribers and you are opting them in using a keyword, utilize short code 444999 even if the keyword you want is not available.  We are sure you can brainstorm an alternative.

A sample flow:

<p style="margin-left: 60px;">
  <p="margin-right: 120px;">
<b>Subscriber Handset:</b> {Keyword} to 345345
<br>
<b>Short Code:</b> You Opted-in to {Store Name} {Program Name}!<br> Msg&Data rates may apply.  <br>{Message frequency}<br> Reply HELP for help, STOP to cancel.<br>
For Age Verification please reply with a hash tag in front of your age. (E.G. #25).<br>
<b>Subscriber Handset:</b> #25
<br>
<b>Short Code:</b> Thank you!  Please tell us your zip code with a hash tag in front.  (E.G. #95107).<br>
<b>Subscriber Handset:</b> #60015
 
## Keywords Cost?
Remember, there is no charge for keywords that you use in your internal 2-way messaging decision trees.  Only keywords leased on 444999 or 345345 will incur any cost.  So feel free to ask away after the subscriber opts-in to recurring messaging.


# The cloudwi.re Short Code Concept
cloudwi.re is not your typical shared short code platform and is built to support guaranteed 2-way messaging.  This concept is supported by our US Patent and a stack of multiple short codes.  There are a total of five short codes in the stack.  This gives the cloudwi.re SMS API a host of advantages over any single shared short code vendor.  To better understand how and why, read on.

## Short Code Classes
cloudwi.re maintains two classes of short codes.  Pay attention to how they differ.  They are as follows:

#### Keyword Marketing Short Codes (345345 & 444999)
If your application will be making use of a keyword, you may skip this section on the keyword marketing short codes as your subscribers will only interact with the communication short codes.  

<b>Standard Marketing Short Code (444999)</b>:<br>
The standard marketing short code, 444999, is utilized solely for keyword marketing.  These keywords can be used for app distribution, couponing or they can be used to opt-in to a particular store.  Recurring 2-way messaging between opted-in subscribers and the store NEVER occurs on a standard marketing short code (I.E. 444999)

It's additionally important to note that an opt-in event that is driven by a keyword to a standard marketing short code will trigger a response from a communication short code. 2-way messaging will then continue on the assigned communication short code.  Opt-ins on this short code guarantee 2-way communication with the store and the subscriber.

<b>Sticky Marketing Code (345345)</b>:<br>
The sticky marketing code, 345345 works a bit differently.  2-way messaging between the opted-in subscriber and the store <b>can</b> occur on this short code.  By default, a subscriber using an opt-in keyword sent to 345345 will be binded to the store with 345345.  HOWEVER, if the subscriber is opted-in to another account or store on 345345, they will be assigned to a new short code for 2-way messaging.  

#### NOTE
We built the sticky code to give Clients the option of holding most SMS communication on just one code.  However, if you are planning a keyword campaign and then doing natural 2-way communication with subscribers after opt-in, we highly recommend that you select your keywords on short code 444999.  It's possible that subscribers can opt-in to other stores if they are sending traffic back on 345345 on a consistent basis.  Make sure you ask yourself that question before selecting a keyword and don't hesitate to contact us if you aren't sure!

There are two short codes in this class.  444999 is throttled at 100 messages per second (MPS) and 345345 is throttled at 200 MPS. 

## A Quick Note about Keywords in Canada
We love Labatt's Blue here.  And if you want to advertise keywords up North to the hockey lovers you can do so on Canadian Long Codes.  cloudwi.re maintains four Canadian long codes for keyword campaigns. However, all of them behave like short code 444999.  We do not offer Canadian Sticky long codes like 345345 in Canada due to filtering concerns.  But, if you wish to ignore this advice you can certainly contact us, and we can enable one for you.  Just understand that fixing carrier filtering issues is a very low priority for us.

In order to utilize keywords on any of the four long codes you <b>MUST</b> create keywords on them via the API using the below long codes as the 'shortCode' value.  Pass them to the API in the following example format: '16477992400'  

### Canadian Marketing Keyword Long Codes (Like 444999)

(587) 319-2400<br>
(647) 799-2400



#### Communication Short Codes (24411, 36546 & 55398)
The communication short code is utilized for 2-way recurring messaging between opted-in subscribers and the store.  When a subscriber opts-in either from an API request or a keyword on 444999, they are assigned and binded to one of the three communication short codes.  Only global compliance keywords work on the communication short codes.  This means that a subscriber cannot opt-in via a keyword to any of these three short codes.

If a subscriber is opted-in and binded to the sticky code (345345) and then attempts to opt-in to another store using a keyword reserved on 345345, the SMS API will assign a communication short code to bind that subscriber to the store.  

There are three short codes in this class and each is throttled at 200 MPS.


## When a Subscriber is Opted-in to More Than 3 Stores
In the event that a subscriber is opted-in to 3 (If 345345 is included it would be four stores) or more stores thus using up their allotment of short codes, the SMS API then starts using long codes to bind the subscriber to that store.  This even is somewhat rare and only generally affects developers.  As cloudwi.re continues to grow and we run into more subscribers opting into multiple stores, we will add short codes to our pool of communication short codes.

## Load Balancing Opt-ins
The other advantage of our patent is that we load balance opt-ins on the cloudwi.re communication short code stack.  The store concept guide outlines how we load balance opt-ins.  But one of the key takeaways is that if you opt-in thirty-thousand subscribers to a store, the cloudwi.re SMS API will just about evenly balance that opt-in load to the three communication short codes through a round-robin process.  It's not a perfect balance due to a few different reasons.  But it will be relatively close.  The end result is the pooling of our bandwidth on those three short codes which reduces message latency and increases campaign speed.

## Message Bandwidth and Queueing
cloudwi.re maintains two classes of messaging queues.  They are as follows:

<b>Single Messaging Class</b>:<br>
This class is reserved for individual messaging to one subscriber.  This could be an opt-in or a responder keyword message reply, or you could just be asking a subscriber what they want to order.  Even mass sign-up notifications that are coming in to your application one by one at a high rate will use this class for the reply message.  

For this class, the SMS API holds open one dedicated queue of 250 MPS (Communication Codes: 50 MPS per code per queue---Sticky Code: 100 MPS per queue) of throttle per short code to keep message latency low.  This throttle is held open regardless if large outbound campaigns are running.

<b>Campaign Messaging</b>:<br>
This class is for sending an SMS/MMS campaign to many subscribers.  The messages may be the same or customized to each subscriber.  For campaign messaging the SMS API holds open two dedicated queues throttled at 275 MPS each (Communication Codes: 75 MPS per code per queue---Sticky Code: 50 MPS per queue).  Campaigns are queued up in the order received.  

The maximum potential for each of the two campaign queues are 275 MPS....or roughly around 16,500 messages per minute.  However, bandwidth will be reduced when developers segment opt-ins out of their database for a campaign. That segmented data taken could have a higher occurrence on one or two communication short codes rather than even dispersal on all three.  Those occurrences are generally rare.  However, when it does occur, the minimum campaign bandwidth is around 75 MPS.  

<b>Messaging Methods</b>:<br>
Please pay close attention to the messaging resource in the API docs.  If you are going to send any bulk outbound messaging campaigns, you must use the campaign methods.  If you begin utilizing the one-to-one messaging methods to send outbound campaigns you will be contacted and asked to move that traffic to the campaign methods.  If you do not comply, we will throttle your concurrency down to a drip.  We understand and totally get that large event sign-ups could lead to higher traffic events that must use the single messaging classes to deliver your messages.  Please work with us to throttle that type of traffic on your end to no more than 15 requests per second.  If that's a no go, then we would advise that you use the campaign methods to collect up those notification events and take advantage of the Hight throttle allotment in campaigns.  We offer three ways to send bulk message campaigns and we are sure that one of them would satisfy your needs.  Contact us to discuss and we'll walk you through the best way forward.  


# Terms Glossary

<table >
<tr>
<td><b>Term</b></td>
<td ><b>Description</b></td>
<tr>
<td >Account (accountId or Parent)</td>
<td>Your main account with cloudwi.re which can be used to create and manage stores or sub-accounts under.</td>
</tr>
<tr>
<td >Assignable (Communication Short Codes)</td>
<td>Cloudwi.re reserves a handful of short codes to ensure and guarantee two way messaging between a store and an opted-in subscriber. These short codes are <b>NEVER</b> used for opt-in or responder keywords.</td>
</tr>
<tr>
<td >Campaign</td>
<td>A mass or bulk text message blast to multiple opted-in subscribers of a store.</td>
</tr>
<td >Carriers</td>
<td>Mobile telecommunications companies like Sprint, AT&T, Rogers, Bell or Verizon.</td>
</tr>
<tr>
<td >Double Opt-In (2 Step Opt-In)</td>
<td>Sometimes referred to as two step opt-in, this opt-in method requires the consent of the mobile subscriber who will receive and opt-in request. Before any additional messages can be sent, the mobile subscriber must reply YES to the opt-in request. It is generally required for non-handset initiated opt-ins, such as from a web form or phone call. The SMS API will automatically deliver the opt-in request template to the subscriber.  If the subscriber then replies Y or YES, the SMS API will deliver the confirmation template.
</td>
</tr>
<tr>
<td >Locked</td>
<td>If single opt-in is attempted three times to a subscriber with no response the opt-in status of the subscriber is changed to locked.  A locked subscriber cannot receive messages from the store except in the event of a handset initiated keyword.  If this creates any issues, please contact Support. </td>
</tr>
<tr>
<td >Long Code</td>
<td>A 10 digit telephone number (somtimes longer with international numbers) that can be used solely for sending and receiving SMS.  cloudwi.re utilizes long codes when a subscriber is on an unsupported short code carrier or when certain errors arise.  They are also used for international messaging.</td>
</tr>
<tr>
<td >Marine Corps</td>
<td>Mother Green's Machine founded in 1775......in a bar people!  cloudwi.re was founded by and employs several former US Marines.  If you are wondering why we use terms like 'go fasters', 'moonbeam', 'silver bullet' and 'AT-4' you are now in the know.</td>
</tr>
<tr>
<td >Marketing Short Code (Opt-in or Responder Short Code) (444999)</td>
<td>A short code Sub-class the cloudwi.re SMS API uses to accept handset initiated opt-in and responder keywords. Keywords recognized by our system will generate the response created by the developer. It is <b>NEVER</b> used for 2 way communication between the opted-in subscriber and the store.</td>  Keywords on short code 444999 should be utilized for applications running natural 2-way recurring messaging between the store and subscriber.
</tr>
<tr>
<td >Sticky Marketing Short Code (Opt-in or Responder Short Code) (345345)</td>
<td>Another short code Sub-class the cloudwi.re SMS API uses to accept handset initiated opt-in and responder keywords. Keywords recognized by our system will generate the response created by the developer. By default, opted-in subscribers will be binded to this code unless a pre-existing bind exists.  If that is the case, the subscriber will be assigned to communicate with the store on one of the communication short codes.  It is not recommended for applications doing recurring 2-way messaging between the store and subscriber.  It is better suited for campaigns that are sending outbound subscriber messaging.</td>
</tr>
<tr>
<td >mobileId</td>
<td>The unique mobile number of a subscriber and the primary identifier in the cloudwi.re architecture.
</td>
</tr>
<tr>
<td >Mobile Originated (Inbound Message)</td>
<td>An SMS or MMS sent from a mobile subscriber to the store.</td>
</tr>
<tr>
<td >Mobile Terminated (Outbound Message)</td>
<td>An SMS or MMS sent from a store to a mobile subscriber.
</td>
</tr>
<tr>
<td >Multi-Media Message (MMS) (Picture Message)</td>
<td>An image sent to/from a mobile subscriber to a store.  This image can be a picture, audio or video, although for now, cloudwi.re only supports pictures in .jpg, .gif or .png formats.
</td>
</tr>
<tr>
<td >New</td>
<td>cloudwi.re assigns a subscriber who has sent a responder type keyword to a store but has never opted-in or out of that store a status of 'new'.
</td>
</tr>
<tr>
<td >Opt-in Keyword</td>
<td>When initiated by the mobile subscriber the opt-in keyword opts them into a store for further SMS communication. It uses the single opt-in process. The cloudwi.re SMS API assigns a dedicated short code to that customer’s mobile number to which they will always communicate with that store through the life of their opt-in.
</td>
</tr>
<tr>
<td >Opted-out</td>
<td>A mobile subscriber who is opted-out from your store and cannot receive any messages other than the opt-in request. The SMS API will automatically deliver the opt-in confirmation template.
</td>
</tr>
<tr>
<td >Pending</td>
<td>A mobile subscriber who has received the opt-in request message but has not responded YES. Until the subscriber responds YES no text messages can be delivered to them.
</td>
</tr>
<td >Responder Keyword</td>
<td>When initiated by the mobile subscriber the responder keyword will respond with only one text message. The mobile subscriber will not be opted-in and no further message can be sent except for the opt-in request or confirmation. It is usually used for promotions or general information. You can use internal responder keywords within your application after the mobile subscriber is opted-in.
</td>
</tr>
<tr>
<td >Segment</td>
<td>Segments are utilized to keep track of SMS and MMS billing.  For SMS, in most cases, segments are counted in 160 character increments.  If you send a message that is 180 characters, it will appear as 2 SMS segments and bill as 2 SMS.  For MMS, each URL is counted as a segment, but you can only send 1 MMS segment at a time.
</td>
</tr>
<tr>
<td >Short Code (Short Numbers)</td>
<td>A 5 or 6 digit number that allows a text message to communicate with a software application. Short codes allow for higher bandwidth delivery of messages.  They are pre-approved by the carriers making them a better choice for higher volume messaging than long codes.
</td>
</tr>
<tr>
<td >Single Opt-In (1 Step Opt-In)</td>
<td>Used primarily when the mobile subscriber initiates and opt-in keyword to 444999 from their mobile device. This opt-in method does not require any additional actions by the mobile subscriber. The mobile subscriber receives a confirmation that they have opted-in to the store and the store can now communicate freely with that subscriber. The cloudwi.re SMS API automates this process and delivers the opt-in confirmation template.  The SMS API can also deliver a single opt-in confirmation without the subscriber initiating it through a keyword.  
</td>
</tr>
<tr>
<td >Short Message Service (SMS)</td>
<td>A text message. "Just text me dude!" That notification your parents get on their phones because you don't call anymore.  
</td>
</tr>
<tr>
<td >Store (Sub-Account or storeId)</td>
<td>Sometimes referred to as sub-accounts or child accounts, the store is basically a bucket to house opted-in customers in. It allows the cloudwi.re SMS API to properly route text messages to and from the store and is used by the developer to tell the SMS API which store you wish to administrate when calling.
</td>
</tr>
<tr>
<td >Subscriber</td>
<td>A person with a unique Mobile ID.  All things equal though, a subscriber and Mobile ID are essentially the same thing.  #Semantics
</td>
</tr>
</table>

# Understanding Keywords
Many of you have come to cloudwi.re for keyword campaigns.  Keywords are initiated by mobile subscribers.  They tell cloudwi.re what the subscriber is looking for or what store they wish to opt-in too.  

## Note
Keywords are not case sensitive.  While we recommend advertising them in all caps, you do not need to reserve them as such....or you can.  Regardless, it doesn't matter.

A friendly reminder, keywords created on cloudwi.re will only work on the marketing short codes 444999 and 345345 and their Canadian long code counterparts.

There are three types of keywords maintained in the cloudwi.re SMS API.  The developer can choose to control only the opt-in and responder keywords.  cloudwi.re retains automation rights over any STOP or HELP request.  The three types of keywords are:

## Opt-in Keyword
This keyword, when initiated by a mobile subscriber will immediately opt them into the store that the keyword is assigned too.  The mobile subscriber will thus be known as an opted-in subscriber to the store and cloudwi.re will assign a dedicated short code for the store and subscriber to communicate with for the life of the opt-in.  Since the subscriber is opted-in, you now have permission to send recurring messaging.

Developers are free to respond to opt-in keywords dynamically if it is so desired via a settings toggle in method Edit Store Settings.

## Responder Keyword
cloudwi.re also provides the ability to set a keyword as a responder only.  When initiated by a mobile subscriber, the responder keyword can only return ONE response.  The response comes from the keyword short code (345345 or 444999) that the keyword is assigned too.  There is no change to a subscriber's opt-in status when this keyword type is triggered.  It is generally used for marketing initiatives, link driving, app downloads, one-time coupons or general information requests. 

Responder keyword responses can be automated by the SMS API  or you can respond dynamically if you wish.

## Global Compliance Keywords
For compliance reasons, the following keywords cannot be reserved.  They are; STOP, END, QUIT, UNSUBSCRIBE, ARRET, CANCEL, HELP, INFO, AIDE, YES, YEA, YEAH and NO.  These keywords are automated by the cloudwi.re SMS API for compliance purposes.  

## Keywords with Spaces
cloudwi.re also supports registering keywords with their natural spaces.  Many campaigns involve natural two word keywords (Like GOBUCKEYES), which comes with subscriber loss and frustration risks due to auto-correct.  To account for the example above, you can register both GOBUCKEYES and GO BUCKEYES as your keywords.  

To state the obvious, yes, that means you're paying cloudwi.re for two keywords instead of one.  And true, we like money, but that amount of money is minimal compared to the cost of one radio spot.  This gives your creative team the difficult task of how to market the keyword versus what to do when folks get upset because they couldn't get their offer.  It's cheap insurance.  No leads are lost due to auto-correct or consumer confusion.

You can register both opt-in or responder keywords with spaces.  

## Wild Carding Keywords
cloudwi.re also supports wild card keywords. For example, let's say you register keyword CLOUD to one of the marketing short codes, 444999. Any message received to 444999 with the keyword CLOUD will be posted to your store. But so will the rest of the body of the message.....as long as there is a space after the initial keyword! So......if a subscriber sends you CLOUD WIRE or CLOUD IS GREY, the SMS API will post both messages to the store you registered keyword CLOUD with.

Wild card keywords are best used for asking subscribers to text a keyword and then a space followed by either an email address or a coupon code.

There is no charge for wild carding! So in the above example, only CLOUD is a billable keyword.  Additionally, wild carding works for both opt-in and responder keyword types.  

## Keywords & Inbound MMS
A keyword will work normally if you are running a campaign that asks the subscriber for a picture.  For example, you have keyword BUCKEYE for Buckeye Pizza.  You want to generate opt-ins by asking subscribers to opt-in with keyword BUCKEYE to any of the marketing short codes.  You also want them to send a picture of them eating Buckeye Pizza wearing their Ohio State gear.  It could be for a contest or social media campaign.  

The inbound keyword will post to your URL along with the image link.  cloudwi.re will then treat the keyword as it would normally with any opt-in or responder keyword.

## Keywords After a Subscriber is Opted-In
It’s important to note that you can create keywords within your application as well, <b>but only AFTER the subscriber has opted-in to your store</b>!  If you want to do responder games or surveys, use the opt-in keyword or Send Opt-In method as your first path to get the mobile subscriber opted-in.

Once done, you can assign any keywords (except for the global compliance keywords) outside of the cloudwi.re SMS API because the subscriber is already opted-in to your store.  You can use the inbound listener to listen for the keywords you want to respond to.  There is no keyword charge for internal keywords because they are not registered to the marketing short codes.  

Reminder though, we don't recommend this with subscribers that are opted-in on short code 345345.  

# Number Formatting-International SMS
The cloudwi.re SMS API ONLY supports messaging to the <a href="https://en.wikipedia.org/wiki/E.164">E.164 Numbering Format</a> with a caveat that the + in front of the number is not accepted.  This format is the internationally-standardized format for all phone numbers, and it includes all the relevant information to route calls and SMS messages globally. E.164 numbers can have a maximum of fifteen digits and are usually written as follows: [country code][subscriber number including area code]. 

A good reference to find a country’s calling code is this <a href="https://en.wikipedia.org/wiki/List_of_country_calling_codes#Alphabetical_listing_by_country_or_region">Wiki Page</a> that lists countries and their calling codes.

For example, to convert a US phone number like 415-100-1000 to E.164 format, you need to add the country code (which is 1) in front of the number so it will be sent to the SMS API as '14151001000'. 

In the UK, and many other countries internationally, local dialing requires the addition of a ‘0’ in front of the subscriber number. 

<b>However</b>, to use E.164 formatting, this ‘0’ must be removed. A number such as 020 7183 8750 in the UK would be formatted as '442071838750' when sent to cloudwi.re.

cloudwi.re provides an E.164 lookup tool via the API.  It's free to use it if you need to!  Any request you make involving messaging that does not pass the E.164 check will synchronously error out in your echo.

## US Short Codes Carrier Support
For now and the foreseeable future, cloudwi.re only maintains short codes in the United States.  When a message is sent to a subscriber on a short code supported carrier, a short code will be used.  If the message is sent on a non-supported short code carrier, the SMS API will select a long code.  In the USA, those carriers are as follows:

<b>Major carriers</b>: AT&T, Verizon Wireless, Sprint, and T-Mobile USA.

<b>Minor carriers</b>: Advantage Cellular (DTC Wireless), Aio Wireless, Alaska Communications Systems (ACS), Appalachian Wireless (EKN), Bluegrass Cellular, Boost Mobile, Carolina West Wireless, CellCom, Cellular One of East Central IL (ECIT), Cellular One of Northeast Arizona, Cellular One of Northeast Pennsylvania, Chariton Valley Cellular, Cricket, Coral Wireless (Mobi PCS), Cross, C-Spire (CellSouth), Duet IP (Maximum Communications New Core Wireless), Element Mobile (Flat Wireless), Epic Touch (Elkhart Telephone), GCI, Golden State, Google Voice, Hawkeye (Chat Mobility), Hawkeye (NW Missouri), Illinois Valley Cellular, Inland Cellular, iWireless (Iowa Wireless), Keystone Wireless (Immix Wireless/PC Man), Metro PCS, Mosaic (Consolidated or CTC Telecom), MTA Communications , MTPCS (Cellular One Nation), Nex-Tech Wireless, NTelos, Panhandle Communications, Peoples Wireless, Pine Cellular, Pioneer, Plateau (Texas RSA 3 Ltd), RINA, Sagebrush Cellular (Nemont), SI Wireless/Mobile Nation, Simmetry (TMP Corporation), SouthernLinc, SRT Wireless, Thumb Cellular, Union Wireless, United Wireless, U.S. Cellular, Viaero Wireless, Virgin Mobile, and West Central (WCC or 5 Star Wireless).

MMS-enabled US short codes are able to deliver MMS messages to the following mobile phone carriers: AT&T, Verizon Wireless, Sprint, and T-Mobile.  For carriers that do not offer MMS support, cloudwi.re will use long codes to deliver your MMS message.

<b>Puerto Rico</b>: Puerto Rico is supported in the US on only 3 of the 4 major carriers. However, delivery is not guaranteed. Supported carriers are: AT&T, T-Mobile and Sprint. Verizon is not supported.  cloudwi.re will generally select long codes to send to Puerto Rico. 

## Canada Opt-in Communications
The cloudwi.re SMS API retains a robust amount of Canadian long codes to support sending up to 24 messages per second in Canada. MMS is supported on the major Canadian carriers.

## Canadian Keyword Long Codes
A reminder, cloudwi.re maintains two Canadian long codes for keyword campaigns that act like 444999.

In order to utilize keywords on any of the two long codes you <b>MUST</b> create them as keywords via the API using the below long codes as the 'shortCode' value.  

### Canadian Marketing Keyword Long Codes (Like 444999)

(587) 319-2400<br>
(647) 799-2400

## Other Countries
cloudwi.re short codes are only available to USA mobile subscribers.  

However, cloudwi.re additionally carries communication long codes (SMS Support Only!) in the following countries:

Canada,
United Kingdom,
Belgium,
Sweden,
France,
Puerto Rico,
Estonia,
Lithuania,
Latvia,
Poland,
Spain,
Germany,
Malaysia,
Netherlands,
Austria,
Australia,
Croatia,
Ireland,
Switzerland,
Chile

As stated, mobile subscribers in these countries cannot opt-in on a cloudwi.re short code.  However, you can utilize the Send Opt-In method to initiate communication with subscribers in the above stated countries.  When you do so, cloudwi.re will automatically select the country matched long code to deliver the message and that long code will now act as the binded 2-way communication code for all SMS between the store and that subscriber.

MMS is not supported outside of the USA/Canada.  We recommend that you send links when communicating SMS outside of the USA/Canada.

## Other International Locations
Other than what is mentioned above, cloudwi.re carries global enabled USA long codes that can send messages to nearly every country in the world.

Bear in mind that sending messages to subscribers in Peru or South Africa from a US Mobile Number can increase the expense for those respective subscribers to receive them in those countries.  If you intend to send higher volumes to any country other than what is listed above, please contact <a href="mailto:support@cloudwi.re?Subject=I%20Need%International%Long%Codes" target="_top">support</a>.  

Tell us the country you need and the projected volume.  It's a simple task to add both marketing and communication long codes to the SMS API from the country codes you wish to send messages too.

## Alphanumeric Sender ID
Alphanumeric Sender ID is not supported in the United States and Canada due to compliance concerns by the carriers.  Additionally, cloudwi.re does not support it outside of North America. 

# Understanding the Opt-In Process
In order to send recurring messaging to a mobile subscriber, the subscriber must be opted-in to a store to receive those messages.  The cloudwi.re SMS API is built to keep you compliant.  However, the developer may choose how they want to opt-in subscribers in the Send Opt-In method.  We highly recommend reading all compliance guides.

As a reminder, if you are sending alerts such as banking notifications or appointment reminders, you can contact us at <a href="mailto:support@cloudwi.re?Subject=Notifications%20anyone?" target="_top">support@cloudwi.re</a> to enable one-time alerts that do not require an opt-in confirmation.

To see flow charts of the opt-in/out process with or without keywords, click <a href="https://cloudwire.gelato.io/guides/categories/architecture-message-flow-diagrams" target="_blank">here.</a>

## Single Opt-In (Handset Initiated)
Single opt-in does not require any additional actions by the mobile subscriber. The mobile subscriber receives a confirmation that they have opted-in to the store and the store can now send recurring messaging. The cloudwi.re SMS API automates single opt-in and delivers the opt-in confirmation template.

A single opt-in can be generated in two ways.  First, the subscriber can send a mobile originated keyword to one of the marketing short codes.  If that keyword is designated as an opt-in keyword, an opt-in confirmation message will be delivered to the subscriber.  That compliant message flow and confirmation language will look like this:  

<p style="margin-left: 60px;">
  <p="margin-right: 120px;">
<b>Subscriber Handset:</b> {Keyword}
<br>
<b>Short Code:</b> You Opted-in to {Store Name} {Program Name}!<br> Msg&Data rates may apply.  <br>{Message frequency}<br> Reply HELP for help, STOP to cancel.
</p>
The “program name” should be a single word to define the kind of alerts, e.g. “Account Alerts,” “News Alerts,” “Coupons” etc.  

The message frequency must be specific, but can be any interval, for example: “1 msg/day,” “4 msgs/month,” “2 msgs/transaction,” etc. If the message frequency will vary based on user interaction, “1 msg/user request” is standard.

## Single Opt-In (Non-Handset Initiated Via the SMS API)
The second way is via the API using Send Opt-In.  The flow is similar to what you just read above, except the subscriber did not initiate an opt-in keyword to the keyword short code.  The Send Opt-In method looks up the subscriber's current opt-in status.  If there is no previous subscriber status for the subscriber's mobile number then an opt-in confirmation message is fired to the subscriber and the subscriber's status is changed to opted-in.  Single opt-in via the API requires express written consent from the subscriber to be opted-in.  Except in instances where you capture express written consent, such as a paper form or in employment Agreements, cloudwi.re highly recommends using the double opt-in process.  Consult your Legal Advisors if you have questions.  

In both instances above, recurring messaging may now occur between the subscriber and the store. 

## Non-Handset Opt-in (Double Opt-in)
Sometimes referred to as two step opt-in, this opt-in method requires the consent of the mobile subscriber via an opt-in request message.

When a user initially signs up by any means other than from a mobile handset, or when express written consent isn't available, a double opt-in process is required. In the Double opt-in, an opt-in request is sent to the subscriber.  The subscriber is now in pending status.  

In order to complete the opt-in process, the subscriber must take action and reply on their handset with a YES or Y to the opt-in request.  After that event takes place, an opt-in confirmation is sent, and the subscriber's status is updated to opted-in.  Recurring messaging can now occur between the subscriber and the store.  A compliant message flow and request/confirmation language will look like this:

<p style="margin-left: 60px;">
  <p="margin-right: 60px;">
<b>Short Code:</b>{Store Name} {Program Name}. <br>Reply YES to opt-in. <br>Msg&data rates may apply.<br> {Message frequency} <br>Reply HELP for help, STOP to cancel.
<br>    
<b>Subscriber Handset:</b> Yes
<br>
<b>Short Code:</b> You Opted-in to {Store Name} {Program Name}!<br> Msg&Data rates may apply. <br> {Message frequency}<br> Reply HELP for help, STOP to cancel.
</p>
The “program name” should be a single word to define the kind of alerts, e.g. “Account Alerts,” “News Alerts,” “Coupons” etc.  

The message frequency must be specific, but can be any interval, for example: “1 msg/day,” “4 msgs/month,” “2 msgs/transaction,” etc. If the message frequency will vary based on user interaction, “1 msg/user request” is standard.

## Understanding Subscriber Opt-in Status
There are four subscriber status categories within the SMS API that are important to understand for recurring messaging.  

### Opted-In
A subscriber who is <i>opted-in</i> can receive recurring messaging from the store.  The subscriber can opt-in using an opt-in keyword, or can be opted-in via the SMS API via single or double opt-in.  In the double opt-in, a request is sent to the subscriber to opt-in.  The subscriber must reply YES or Y in order to complete the opt-in.

### Opted-Out
The subscriber who is <i>opted-out</i> cannot receive recurring messaging from the store.  If a message is attempted to an opted-out subscriber using Send Message or Send Campaign, the SMS API will block that message and notify you asynchronously that the subscriber is not opted-in.  Additionally, an opted-out subscriber can only be opted-in again using double opt-in or by sending in an opt-in keyword belonging to the store.

The opted-out subscriber can opt back in using an opt-in keyword at any time.  They can also send Responder keywords.  However, if the subscriber is to be opted back in via the SMS API, Double opt-in is required.  The API will send a notification webhook when that event occurs, so you know what action to take.

### Pending
The subscriber who is <i>pending</i> has received an opt-in request but has not replied YES or Y to it to complete the opt-in process.  If a message is attempted to a pending subscriber using Send Message or Send Campaign, the SMS API will block that message and notify you asynchronously that the subscriber is pending.  However, you may retry Send Opt-In (The Double Opt-in) again up to 3x to initiate a YES or Y response from the subscriber. After 3 attempts, the subscriber's status is updated to locked.  

The pending subscriber can opt-in using an opt-in keyword at any time.  They can also send Responder keywords.  

### Locked
The subscriber who is <i>locked</i> has received an opt-in request from the store 3 times but has failed to reply YES or Y to the request and complete the opt-in process.  Additionally, the subscriber may reply NO or N to a double opt-in request which will also lock their status.  If a message is attempted to a locked subscriber using Send Message, Send Campaign or Send Opt-In, the SMS API will block that message and notify you asynchronously  that the subscriber is locked.  However, a locked subscriber can still initiate both opt-in and responder keywords to the SMS API.  Initiation of an opt-in keyword will opt the subscriber back in and remove the locked status.

In certain cases, a subscriber can get confused and accidentally lock themselves.  In that event, please <a href="mailto:support@cloudwi.re" target="_top">contact us</a> and we can help.  

# Authentication-Concurrency-Security
The SMS API returns synchronous and asynchronous data in JSON only.

## Authentication
When signing up with cloudwi.re you'll establish an email address as your primary account ID username.  cloudwi.re will also issue you an <i>accountId</i> and JSON authentication token as well.  The token can be found in your administrative panel and is passed to the SMS API within the header of the request.  It is also available via API request which you'll find in the API reference. 

## Base URL
The cloudwi.re SMS REST API is served over HTTPS and available via the following base URL for each request.

```javascript
https://moonbeamapi.cloudwi.re
```

## Request Formatting
Although not required, cloudwi.re advises you to set the following in the header of the request: 

```javascript
--header 'accept: application/json' \
--header 'content-type: multipart/form-data; boundary=---011000010111000001101001' \
```

## Token
Pass your token in the request header as follows:
```javascript
authorization: Bearer Token
```
## Web Apps
Our sample code only shows authentication being passed in the header.  However, for those of you building web apps that struggle with different browser issues related to passing authentication in the header, we do allow the token to be passed in the URL of the request.  No header required.  An example of how to pass the token in this instance is as follows:

```javascript
https://moonbeamapi.cloudwi.re/account/addstore?token=T0KENHERE
```

## Create a Store
You <b>MUST</b> create a store before you can send or receive any messages with a mobile subscriber!

```javascript
curl --request POST \
  --url 'https://moonbeamapi.cloudwi.re/account/addstore' \
  --header 'accept: application/json' \
  --header 'authorization: Bearer SOME.JWT.TOKEN' \
  --header 'content-type: multipart/form-data; boundary=---011000010111000001101001' \
```

After you create a store, a <i>storeId</i> will be issued to you.  In most calls to the SMS API the <i>storeId</i> will be required in the method parameters so that we know which store you wish to administrate.  You can now opt-in subscribers and send/receive messages.

## Concurrency
Each cloudwi.re account is limited to 100 concurrent requests per second.  If you exceed your concurrency limit, cloudwi.re will respond with a '429' fail code and drop the request.  You are free to retry it. 

Concurrency limits can be raised for large keyword campaigns. 

## USA based API Response Times
Response time averages vary due to the nature and payload return of the request, the location from where it is made and bandwidth speeds.  For read specific requests that involve finding one record, such as information on an individual subscriber or keyword, response times generally average 120-400ms.  Some read requests such as campaign delivery status or subscribers by store will pass 100 records per page and that will increase average response times to about 900-2000 ms.  

For write specific requests, such as sending messages or creating keywords, response times generally average 120-500ms.

For requests such as Send Campaign (The Batch Methods), which could have a sizable string, that response time will be increased depending on the amount of numbers and messages within the array.  Please keep the above in mind when setting time outs.  If you connect to the SMS API to deliver a campaign of 5k messages it's going to take a little bit for cloudwi.re to consume the request.  Plan accordingly. 

## Data and Payment Security
When signing up for cloudwi.re, you'll note in the terms & conditions you read that we do not resell any data that is posted or received to our service.  Ok...ok....Just kidding!  We know you didn't read them!  But hey, who does?  You can here:    But it's important to us that you know this.  We're here to provide compliant short code messaging.  That's it.  The data that we maintain is only mobile numbers and their status.  Any additional data details are acquired from 3rd party vendors (Such as the intel methods) and are not stored by cloudwi.re.  We fire it to you and then forget it.

Payment information is handled by a third party and is not stored by cloudwi.re under any circumstances.  Your payment information is passed on to our merchant vendor in exchange for a token to bill your account.  Our merchant vendor is PCI 1 compliant.  

## Token Security
Your AUTH token is required in every request to the API.  If it is compromised, or you believe it has been, you may request a new one in the Admin portal.  Make sure you update your services quickly with the new token.

# Postman-Quick Start
cloudwi.re does not provide an API playground for various spam concerns.  So we recommend Postman.  You probably know about it.  If you don't, get it at www.getpostman.com.  It's a rock solid tool for getting to know APIs.  After you download it, you can make live requests to the SMS API in under one minute.

The API collection is ready to go.  But in order to make the best use of Postman read up on creating an environment.  The SMS API collection will pull data from the environment in order to enable calls to the API.  You can read up on how to create an environment here: <a href="https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments">Creating Postman Environments</a>.

For ease of use, you will want to focus on these main keys and their values.  

Authorization<br>
accountId<br>
storeId<br>

Optionally, you can consider adding the following to make life a little easier:

keywordId<br>
mobileId<br>

It will look as such below.  Just enter your token, account ID and your first Store ID.  Once done, you can then attempt to create a store and start learning the API from there.  Make sure you edit values where you don't see the curly braces like {{accountId}}<br>
<center>![](http://crmtext.com/images/environment.png)</center>

Some sample responses are withheld in our documentation due to ID exposure.

## Most Common Methods
The cloudwi.re SMS API has its most popular methods.  We want to list them out for you for those whose patience level is somewhat challenging.  We're the same way so don't take it personally!

In order to send messages with cloudwi.re you must create a store under your account.  You can do this in the admin portal or via the API.  Go ahead and add your store.  Make sure you add an inbound message listening URL if you want to test 2-way messaging.  You can do that with:

ADD STORE

To enable 2-way communication between a subscriber's mobile device and your application, the subscriber must be opted-in to the store.  Go ahead and opt yourself in or out with:

SEND OPT-IN<br>
SEND OPT-OUT

After opt-in, you'll want to send SMS or MMS. In the 2-way messaging environment, you'll want to use send message.  If you want to send bulk messages to many subscribers you'll want to use Send Campaign, which allows you to pass an array of mobile numbers with corresponding SMS, MMS messages.....or both.  You can also track the status of delivery for those messages.  

SEND MESSAGE<br>
SEND CAMPAIGN<br>
GET MESSAGES STATUS<br>
GET CAMPAIGN MESSAGE STATUS<br>

For keywords, you can create them on either marketing short code using Create Keyword.  If you create a responder keyword and want to manage the responses to them you can use Send Responder Keyword.  Since a responder keyword delivers content to a mobile subscriber REGARDLESS of opt-in status, cloudwi.re requires the Keyword ID to be passed with this particular method.  It's simply there for compliance purposes.  

CREATE KEYWORD<br>
SEND RESPONDER KEYWORD MESSAGE

# Pre-Development Considerations
First and foremost, when you get connected and set up an inbound message listener, please don't send "Test" as a message.  It can create all sorts of problems that require tickets up to the carrier level.  Let's move on!

## Holy Crap I'm Confused.  What do I do?
We are here to help!  Listen, we didn't get to where we are by leaving our Clients to fend for themselves.  Talk to any of our Clients.  All of them.  They will all tell you we are easy to reach, and we'll walk you through your flow.  We get that our product can be a bit hard to grasp even for very smart people.  Don't hesitate to reach out to us with any questions.  We only ask that you come to us after reading the documentation.  Support is always free and we love to answer questions and talk about use cases :)

Our products are architected for messaging.  Even if your questions are architectural, please don't hesitate.  We can walk you through how cloudwi.re is built so you can replicate and provide a solid base for high volumes of messages.

## Prepare your webhooks
At cloudwi.re, we want to be fast.  To do so we process many requests asynchronously.  If your inbound message volume is going to be high, make sure you have a plan in place to balance large amounts of posts from the SMS API.  For now, we limit concurrent inbound webhook events to 50.  We will eventually increase that limit to 100 and possibly beyond.  So make sure you can handle it. <br><br>
We've been doing this for ten years.  We can help estimate what an inbound keyword campaign might generate so you can properly load test.  But if you are giving away 100 grand to the first person who texts your keyword at an NFL game, we suggest you do a lot of load testing.  There are plenty of SaaS tools out there that will allow you to dummy a cloudwi.re post and scale it.  <a href="https://www.loader.io">Loader.IO</a>, and <a href="https://www.loadimpact.com">Load Impact</a> are just a few.

The SMS API is tuned to deliver webhooks at 100 concurrent connections per second. Webhooks are queued up by cloudwi.re. In the event of failure, the queues will simply just keep retrying. So as traffic thins and you start consuming all of your posts you will not lose messages.

However, if that failure is continuous, and then you fix it at 2 in the morning, that could result in your application responding to messages. So make sure you address notifications from cloudwi.re about webhook health as quickly as you can. We will only send you three webhook failure notifications. After that, it's on you.
## Big Event with Big Traffic?
Reach out to us if you are doing keyword marketing at a sporting event.  We like to pre-prepare our infrastructure.  Send us an <a href="mailto:support@cloudwi.re?Subject=I'm%20going%20to%20blow%20up%20your%20server%20bill!" target="_top">email</a> with the date of the event.  We'll add some extra horsepower to make sure everything runs smooth instead of waiting for our auto-scale to kick in.  cloudwi.re is architected to take advantage of our short code bandwidth.  However, our aggregator has no limit on how many inbound messages will be sent to our service.  So a heads-up would be appreciated.  

## Decision Trees or Advanced Logic
The same goes here.  cloudwi.re is a fire and forget system.  Our logic revolves around compliance and what keywords belong where.  If you are doing advanced logic via 2-way messaging and you expect heavy traffic, make sure you load test.  The subscriber expects quick responses from their keywords.  

## Do you Need Multiple Stores?
That's really up to you.  cloudwi.re uses the store concept to essentially create opt-in buckets and take the opt-in logic out of the developer's hands.  If you are running a platform with multiple unrelated sub-accounts (A CRM is a good example) then it's probably a darn good idea.  If you run annual conferences for different industries, it's a good idea.

However, If you are a singular standalone enterprise, then the only reason you might need more than one store is for Dev and UAT or maybe support versus marketing.  There is no cost for additional stores to developers.  

We are always happy to help you answer this question based on our experience.

## Transaction, Store and Keyword IDs
It's important to have a plan to store the above IDs.  Transaction ID's will be used to retrieve message status updates.  Store IDs are used to tell cloudwi.re what store you are wanting to create messages or tasks for.  Keyword IDs are important for responder messaging and keyword deletion.

## How to Send Us Messages
The API supports UTF-8 encoding.  But be careful with special characters.  You can feel free to send plain text or URL encode your message as well.  We will send that on to the carriers for delivery.  

Please take note that when sending individual messages as part of opt-ins, keyword responses, alerts, 2-way messaging or what not, please use the Send Message method.  Even during large sign-up campaigns, the chance of latency issues are very low.

However, if you intend to send a bulk message campaign, please use one of the campaign methods.  They allow you to send campaigns to either all store subscribers or a sub-set with one call to the SMS API.  It creates less load on the API and allows us to properly throttle the messages to the available bandwidth.    

## Timeouts
3 Second timeouts are satisfactory for individual message requests or subscriber look ups.  Creating stores and changing store settings as well as keyword functions will also process quickly. 

However, cloudwi.re allows you to batch campaign requests of up to 5k mobile subscribers per batch.  If you are sending batch outbound message requests to cloudwi.re, the API connection will stay open much longer.  Due to network connectivity and other factors that go into cloudwi.re consuming a large set of data, please plan accordingly.  We're talking minutes!

With regards to larger read requests such as bulk subscriber lookups and campaign delivery reports, the API will generally process that information and return it to you in under 3 seconds.  However, those methods return 100 records per page and we'd recommend setting back to 10 seconds for those larger read requests.  If you are connecting to us from Diego Garcia, then you may want to consider doubling that!

## Message Latency
It's important to note that during peak usage times message latency can occur due to bandwidth constraints.  In most cases message latency occurs on the upstream carriers end where every once in a while the queues stack up and get stuck.  Make sure you sign-up for <a href="at4armed.cloudwi.re">cloudwi.re alerts</a> for those notifications.  

More important, if you are going to run a mobile originated keyword campaign at a large event like a Buckeye football game or a concert then you must prepare yourself or your Client for some mobile terminated latency back to the mobile subscriber.  Again, we are limited via bandwidth.  If a few thousand people hit a keyword within one minute, there will be a handful of seconds before they receive the response.  We can temporarily increase that bandwidth.  But please give cloudwi.re three week’s notice before your campaign is to kick off.  It isn't cheap either, so make sure your Client has the cash.

With regards to MMS, you will notice it isn't quite as snappy to get to your device as an SMS might be.  The difference is the payload.  Receiving an MMS a few seconds after you send one via the SMS API or the UI is perfectly normal.  It takes a little longer to push a 4MB payload through to the device and you can factor in your mobile signal to that equation.

## These Short Codes Confuse Me
They confuse everyone.  So don’t worry about it and let us handle how we assign subscribers to stores.  You do not need to worry about what subscriber is binded to what code for what store.  We handle all of that logic.  

The only thing you need to remember is that when you get a keyword and want to market it, you will promote it on whichever marketing short code you registered it on, 345345 or 444999.

<b>Text KEYWORD to 345345</b>
<b>Text KEYWORD to 444999</b>

## I Might Need My Own Short Code
Although not a core part of our business, cloudwi.re can manage this process for you and host the code on our short code stack.  This allows enterprises to stay compliant without having to build in their own opt-in logic and have free range of keywords.  You can choose to have all communications go out only on your short code, or you can use your short code like we use our marketing short codes.  

You may choose to directly pay for hosting and lease fees or have cloudwi.re manage these for you.  cloudwi.re charges a one-time set-up fee of $1,000 to cover the costs of adding your short code to the SMS API short code stack.  There are no additional mark-ups thereafter.

# What cloudwi.re Automates
The cloudwi.re SMS API manages additional tasks for the developer out of the box.  Some of these features can be disabled and managed by the developer and that is noted where applicable in the sections below.  Read on:

## Automating Double Opt-in
If a developer chooses to send double opt-in, the subscriber will receive an opt-in request message and their status will be changed to pending.  Action must be taken by the subscriber to opt-in.  If the subscriber replies 'Y' or 'Yes' the cloudwi.re SMS API will change the subscriber's status to opted-in and deliver an opt-in confirmation message to the subscriber. 

Additionally, if the subscriber replies 'N' or 'No' to the opt-in request, cloudwi.re will change the subscriber's status to locked and deliver an opt-out confirmation to the subscriber.

## Blocking Single Opt-In to Opted-Out Subscribers
If a subscriber is in an opted-out state and you attempt to opt them back in using single opt-in, the attempt will be blocked.  Opted-out subscribers may only opt back in to your store via a handset initiated opted-in keyword or via double opt-in.

## Blocking SMS to Non Opted-In Mobile Subscribers
The cloudwi.re SMS API will generally not allow text messages to non opted-in mobile subscribers except in very distinct circumstances like handset initiated responder keywords or compliance keywords.  

If your use case requires that you send messages to non opted-in mobile subscribers for alert or other notification use cases, contact <a href="mailto:support@cloudwi.re">support</a>.

## Handset Keyword Automation
<b>Opt-In Keywords</b> <br>
Out of the box, Opt-In keywords will opt a subscriber into the store the keyword is assigned too.  The SMS API will then reply automatically with the compliant store opt-in confirmation template.  No action is required by the developer and the subscriber's status will be updated to an opted-in state.  

For developers who wish to manage the replies themselves, the automation can be disabled.  We don't recommend it, but we do understand that some use cases require dynamic confirmation replies.  STAY COMPLIANT!<br><br>
<b>Opt-out Keywords</b> <br>
The cloudwi.re SMS API will send the compliant opt-out template when we receive a STOP message from the mobile subscriber on the short code for which they are assigned to communicate with your store.  The subscriber will then be updated to an opted-out state.  

STOP replies cannot be managed dynamically and cloudwi.re will retain automation rights to this keyword type.  However, the template can be edited.<br><br>
<b>Responder Keywords</b><br>
Responder keywords can be automated as well if you want to be lazy.  And feel free!  We built this so you could be.  When you create a responder keyword you can then edit its content.  Once done, cloudwi.re will respond to the initiated responder keyword automatically.  However, if you don't store content for the keyword inside of cloudwi.re, you are responsible for managing the replies.<br><br>
<b>Help Keyword</b><br>
The cloudwi.re SMS API will send the compliant help template to the mobile subscriber. The help template includes the program name, how to opt-out and so on.  HELP replies cannot be managed dynamically and cloudwi.re will retain automation rights to this keyword type.  However, the template can be edited.<br><br>
<b>Already Opted-in Alert</b><br>
By default the cloudwi.re SMS API generates a template that notifies the subscriber they are already opted-in if they attempt to opt-in again. For example, let’s say your store keyword is PIZZA and the store name is Jim’s Pizza. 

If a mobile subscriber is opted-in to PIZZA and sends any keyword belonging to Jim's Pizza again 5 months later, the cloudwi.re SMS API will generate a message stating, “You are already opted-in to John’s Pizza.”  This automation is turned on by default but can be disabled or edited in the store resource.

## Inbound Messages Webhook Push (Mobile Originated) 
If you set a callback URL for your store the cloudwi.re SMS API will post all inbound message traffic to it.  We allow one callback URL per store. What we push to this URL is further down in the docs.  

## Notifications URL Webhook Push
cloudwi.re will update some requests asynchronously to your notification URL.  Those include messages sent to an opted-out subscriber or notifications that certain jobs have completed off the queue like store deletion.  We allow one notification URL per store. What we push to this URL is further down in the docs.  

## Unsupported Carrier Short Code SMS
In the event that cloudwi.re detects a send attempt to a mobile number on a carrier that does not support short codes, the SMS API will assign and send the message on a long code.  The subscriber will be binded to that long code for the life of the opt-in or whenever they port to a short code supported carrier.  In the latter event, messages will resume on the assigned short code.

## Long Code on Short Code Fail or Undelivered
Under certain error conditions, cloudwi.re will fire a failed short code message on a long code.  This event normally occurs after receiving 30005 or 30008 errors on a short code attempt.  Other errors may be added as delivery reporting from the carriers becomes more accurate.  

## Unsupported Carrier MMS
In the event that cloudwi.re notes an MMS slated for delivery to a carrier that does not support MMS, the SMS API will convert your MMS into a URL and deliver it as or inside an SMS, linked to the media you sent.  

## UCS2 to GSM Encoding
To prevent your message segment counts from slipping down to 70 characters, cloudwi.re will convert UCS2 characters to GSM to keep you at 160 character segments.  It doesn't always work, so plan accordingly and try and get in the habit of checking encoding before you fire any campaigns.  

## Country Origin of Number
cloudwi.re will take any mobile number that you opt-in and select a local long code to send it on if outside the United States where available.  If not, cloudwi.re will send on a global enabled USA long code.  

# Mobile Intelligence
cloudwi.re strives to provide brands & enterprises additional insights to their subscriber base.  Whether you are running transactional 2-way message applications or running inbound keyword campaigns, cloudwi.re provides tools to help you gain an intelligence advantage to better service and sell your customers.  

## Carrier Intel (Pay Per Request)
A carrier lookup is provided in the Intelligence resource.  The lookup covers North American mobile and landline numbers.  Most international numbers can be looked up with this tool as well.  The returned payload includes the line type and carrier.  You may choose to scrub your existing list, or you can do lookups to ensure high MMS delivery probability.  

Each lookup is billed at $.005 cents per successful request.  Sample Payload:
```json
{
  "status": "pass",
  "code": 200,
  "message": "Subscriber Intel",
  "results": {
    "_id": {
      "$id": "585066f9d16a1047278"
    },
    "caller_name": null,
    "country_code": "US",
    "phone_number": "+19994449999",
    "national_format": "(999) 444-9999",
    "carrier": {
      "mobile_country_code": "310",
      "mobile_network_code": "150",
      "name": "AT&T Wireless",
      "type": "mobile",
      "error_code": null
    },
    "type": "carrier",
    "mCreate": {
      "sec": 1481621049,
      "usec": 0
    }
  }
}
```

## E.164 Intel (Free Per Request)
cloudwi.re can help validate your collected phone numbers for country of origin lookup and the validity of the E.164 format to which your data is housed.  You are free to use this method to check your data for valid numbers and what country they belong too.  Line type is provided in this method, but it is not accurate.  It’s passed on as a courtesy.  For accurate line type, please use the Carrier Intel method.  

## Number Reputation Intel (Pay Per Request)
For developers running commerce applications, cloudwi.re can assist with checking telephone numbers for potentials spam or fraud history and scoring the number based on risk.  Thus, allowing businesses to make more informed selling decisions to prevent fraud.  High risk numbers will be reported with the risk type associated with them.  Numbers are scored on a scale of 1-4 with 4 being the highest risk.  

Each lookup is billed at $.009 cents per successful request.  Sample Payload:

```json
{
  "status": "pass",
  "code": 200,
  "message": "Reputation Intel",
  "results": {
    "_id": {
      "$id": "589dd287d16a10f970199420"
    },
    "caller_name": "foo",
    "country_code": "US",
    "phone_number": "+19994448888",
    "national_format": "(999) 444-8888",
    "carrier": "foo",
    "add_ons": {
      "status": "successful",
      "message": "foo",
      "code": "foo",
      "results": {
        "whitepages_pro_phone_rep": {
          "request_sid": "XRecbc0f4586d35f33bac46c831e0cb335",
          "status": "successful",
          "message": "foo",
          "code": "foo",
          "result": {
            "results": [
              {
                "phone_number": "9994448888",
                "reputation": {
                  "level": 1,
                  "details": [
                    {
                      "score": 4,
                      "type": "Risk",
                      "category": "Voip Scam"
                    }
                  ],
                  "volume_score": 1,
                  "report_count": 1
                }
              }
            ],
            "messages": [
              "foo",
              "foo",
              "foo"
            ]
          }
        }
      }
    },
    "mCreate": {
      "sec": 1486694855,
      "usec": 0
    }
  }
}
```

# Understanding Message Delivery Status
For message status, the cloudwi.re SMS API allows polling of message IDs to retrieve the delivery status of Single Messaging class messages (Remember, those simple 1-to-1 messages like opt-ins, or regular outbound messaging in the single message class).  We recommend setting a timer of at least 5 seconds after you send a message to poll its status.  This allows the carriers to properly notify us of the correct message status. There are sometimes up to six updates to the delivery status.  The SMS API will return an Array of all status updates and their time stamps as it is.

To accomodate for any high volume or carrier lag, cloudwi.re will respond with a 200 and a message noting that your message is still queued and awaiting a carrier update.

## Campaigns
A note about campaigns.  We don't want to bomb your webhooks.  Because of that, cloudwi.re utilizes a different method to retrieve message status for the Campaign Messaging Class.  It's a GET and you can page through your delivery results.  

## Accuracy of Delivery Reporting
It's important to note that the reporting received from the carriers is not always accurate.  Although rare, instances of delivery confirmed messages not arriving at the destination handset do occur.  Unfortunately, there is no real action that you can take other than advising that the handset be hard reset and then try again.

One thing we have seen with frequency is that subscribers toe the line in available memory to the mobile device.  If the device has no memory available, messages cannot be received.  

## Status Descriptions
Below are the status descriptions and what they mean when received in a Get Message Status request. 

<table>
<tr>
<td><b>Status</b></td>
<td ><b>Description</b></td>
</tr>
<tr>
<td>Delivered</td>
<td>cloudwi.re has received confirmation from the carrier, and in some cases the device, that the message has been delivered.</td>
</tr>
<td>Failed</td>
<td>The upstream provider did not accept the message and hence delivery fails.</td>
</tr>
<tr>
<td>Queued</td>
<td>The message is queued at the AGGREGATOR level to be delivered to the mobile subscriber.</td>
</tr>
<tr>
<td>Sent</td>
<td>Once the nearest upstream carrier has accepted the message for delivery to the SMS network, the status is updated to sent.  This status is not a delivery receipt.  The carrier is merely telling us they sent it.</td>
</tr>
<tr>
<td>Undelivered</td>
<td>We received notice indicating that the message was not delivered. This can happen for a number of reasons including carrier content filtering, availability of the destination handset, etc.</td>
</tr>
</table>

The following message delivery error codes will be the most common seen by the developer in the cloudwi.re platform when retrieving delivery status.  It's important to note that some of these errors will not be received from short code attempts. Regardless, receiving one of these errors means that the subscriber did not receive your message.  A sample return body of a Get Message Status request can be found in the <a href="https://cloudwire.gelato.io/docs/versions/moonbeam/resources/messaging">message resource</a>. 

<table>
<tr>
<td><b>Error Code</b></td>
<td ><b>Possible Causes</b></td>
</tr>
<tr>
<td>30003</td>
<td>Unreachable Destination Handset - The destination handset you are trying to reach is switched off or otherwise unavailable.</td>
</tr>
<tr>
<td>30004</td>
<td>Message Blocked - The destination number you are trying to reach is blocked from receiving this message (ex. due to blacklisting).</td>
</tr>
<tr>
<td>30005</td>
<td>Unknown Destination Handset - The destination number you are trying to reach is unknown and may no longer exist.</td>
</tr>
<tr>
<td>30006</td>
<td>Landline or Unreachable Carrier - The destination number is unable to receive this message. Potential reasons could include trying to reach a landline or, in the case of short codes, an unreachable carrier.</td>
</tr>
<tr>
<td>30007</td>
<td>Carrier Violation - Your message was flagged as objectionable by the carrier. In order to protect their subscribers, many carriers have implemented content or spam filtering.  This error will only appear on outbound long code traffic</td>
</tr>
<tr>
<td>30008</td>
<td>Unknown Error - Delivery of your message failed for unknown reasons.</td>
</tr>
<tr>
<td>11751</td>
<td>Media Exceeds Mobile Operator Limit - The specified message media exceeds the maximum size limit for that number's mobile operator.</td>
</tr>
<tr>
<td>21614</td>
<td>'To' number is not a valid mobile number - Not a valid formatted number.  Sometimes occurs when messaging a landline.</td>
</tr>
</table>

# Common API Errors

## Common Synchronous Errors
The following errors can be triggered when calling any method to the SMS API.  In almost all circumstances, cloudwi.re will pass a status of FAIL and error code of 400 or 401 with any error.  cloudwi.re will also pass a detailed message of why your request failed.  

Method specific errors are listed in the API Method documentation further below.

<table>
<tr>
<td><b>Error</b></td>
<td><b>Error Code</b></td>
<td><b>Action Message</b></td>
</tr>
<tr>
<td>Account Suspension</td>
<td>401</td>
<td>Account Disabled due to lack of credit, spam concerns or improper content. Please contact support@cloudwi.re.
</td>
</tr>
<tr>
<td>Invalid API Key</td>
<td>401</td>
<td>Invalid API Key:  cloudwi.re does not recognize your API key or Account ID.  Login to https://gofasters.cloudwi.re to check your API key and Account ID.</td>
</tr>
<tr>
<td>Blocked IP Address</td>
<td>401</td>
<td>Unrecognizable IP Address:  Your IP address has been flagged for troublemaking.  Please contact support@cloudwi.re.
</td>
<tr>
<td>Invalid Method</td>
<td>400</td>
<td>Invalid Method:  Please check to make sure you are sending proper parameters and values.  Please review the developer reference for help:  https://cloudwire.gelato.io/reference/docs</td>
</tr>
<tr>
<td>Invalid Store ID</td>
<td>400</td>
<td>Invalid Store ID:  Please check and try again or login to https://portal.cloudwi.re to check your store IDs. 
</td>
<tr>
<td>Request Limit Exceeded</td>
<td>429</td>
<td>The account is exceeding the allowable requests per second threshold.  Dial it down Captain! But feel free to retry your request.</td>
</tr>
</table>

## Sample Payload
```json
{
  "status": "fail",
  "code": 400,
  "message": "The keyword is not available on the requested short code. Either check availability on another short code or brainstorm a new one.",
  "results": []
}
```

# Webhook Error-Job Notifications
## Asynchronous Errors
Receiving an error to your notification URL means that a message you are attempting did not pass compliance checks and was blocked by cloudwi.re.  A status of 'fail' will be included in the post body.  The errors are duplicated when you retrieve your message status via Get Status.  Additionally, some job completion alerts are forwarded to this URL as well.  

It's important to note, that message delivery errors are not posted to your notification URL.  Those can only be retrieved via Get Status.

The SMS API will deliver notifications to your notification URL in multipart/form-data.  Additionally, cloudwi.re expects a 200 passed back to it in the header once your service has completed the handshake. 


## Possible Errors with Send Opt-In (Single)
<table>
<tr>
<td><b>Notification Message</b></td>
<td><b>Reason</b></td>
</tr>
<tr>
</tr>
<td>The subscriber is already opted-in. No opt-in message was sent because it is not required.</td>
<td>When attempting to use method Send Opt-In (single or double) to a subscriber who is already opted-in.  The subscriber is already opted-in to the store and no opt-in message is required so it was blocked by cloudwi.re</td>
</tr>
<tr>
<td>The subscriber is in pending status and must reply Yes from the double opt-in request before you may send a message.</td>
<td>The subscriber is pending from a double opt-in request and cannot be opted-in via single opt-in until they reply Yes or Y from the double opt-in request.</td>
</tr>
<tr>
<td>No opt-in message was sent. The subscriber is in opted-out status and be must opted-in via double opt-in to resume messaging.</td>
<td>When attempting single opt-in to an opted-out subscriber. If a subscriber has opted-out of your store, double opt-in of that subscriber is required.</td>
</tr>
<tr>
</tr>
<td>The subscriber is locked for too many double opt-in attempts or a NO response from a double opt-in request. No message was attempted. The subscriber must send an opt-in keyword to opt-in.</td>
<td>The subscriber is in a locked status and cannot receive messages.  They must use an opt-in keyword to opt-in.  On rare occasions, this event can be triggered by a confused subscriber and can be rectified by cloudwi.re. <a href="mailto:support@cloudwi.re">Contact us</a> for help if it arises.</td>
</tr>
<tr>
</table>

## Possible Errors with Send Opt-In (Double)

<table>
<tr>
<td><b>Notification Message</b></td>
<td><b>Reason</b></td>
</tr>
<tr>
</tr>
<td>The subscriber is already opted-in. No opt-in message was sent because it is not required.</td>
<td>When attempting to use method Send Opt-In (single or double) to a subscriber who is already opted-in.  The subscriber is already opted-in to the store and no opt-in message is required so it was by cloudwi.re</td>
</tr>
<tr>
</tr>
<td>The subscriber is locked for too many double opt-in attempts or a NO response from a double opt-in request. No message was attempted. The subscriber must send an opt-in keyword to opt-in.</td>
<td>The subscriber is in a locked status and cannot receive opt-in messages.  They must send an opt-in keyword that belongs to the store to opt-in.  On rare occasions, this event can be triggered by a confused subscriber and can be rectified by cloudwi.re.  <a href="mailto:support@cloudwi.re">Contact us</a> for help if it arises.</td>
</tr>
<tr>
</table>

## Possible Errors with Send Message & Send Campaign
<table>
<tr>
<td><b>Notification Message</b></td>
<td><b>Reason</b></td>
</tr>
<tr>
</tr>
<td>The subscriber is currently in Opted-Out status. Reference: https://cloudwire.gelato.io/docs/versions/moonbeam/data-posted-to-your-notification-url</td>
<td>The subscriber is opted-out and cannot receive messages from Send Message or Send Campaign.  Double opt-in is required via Send Opt-In to opt-in the subscriber to recurring messaging.</td>
</tr>
<tr>
</tr>
<td>The subscriber is currently in Pending status. Reference: https://cloudwire.gelato.io/docs/versions/moonbeam/data-posted-to-your-notification-url</td>
<td>The subscriber is pending from a double opt-in request and cannot receive messages from Send Message or Send Campaign until they reply Yes or Y from the double opt-in request.</td>
</tr>
<tr>
<td>The subscriber is currently in Locked status. Reference: https://cloudwire.gelato.io/docs/versions/moonbeam/data-posted-to-your-notification-url</td>
<td>The subscriber is in a locked status and cannot receive recurring messages from Send Message or Send Campaign.  They must send an opt-in keyword that belongs to the store to opt-in.  On rare occasions, this event can be triggered by a confused subscriber and can be rectified by cloudwi.re.  <a href="mailto:support@cloudwi.re">Contact us</a> for help if it arises.</td>
<tr>
</tr>
<td>Invalid URL: Your URL appears to be malformed. Only valid URLs beginning with HTTP:// or HTTPS:// are accepted.</td>
<td>This error is unique to Send Campaign.  Since an array of mobile numbers are passed in a campaign, media URLs are not checked at the request level.  If a bad media URL is received in the campaign this notification will fire.</td>
</tr>
<tr>
</table>

## Asynchronous Updates
The SMS API sends two updates.  One is when double opt-in is attempted to an opted-out subscriber.  The other is for when a store deletion job is completed.
<table>
<tr>
<td><b>Notification Message</b></td>
<td><b>Reason</b></td>
</tr>
<tr>
</tr>
<td>The subscriber was sent an opt-in request. Subscriber status is pending.</td>
<td>A friendly reminder to let you know that a double opt-in attempt to an opted-out subscriber has passed compliance checks and the message was attempted.</td>
</tr>
<tr>
</tr>
<td>The store, and its keywords and subscribers, have been removed.</td>
<td>cloudwi.re S@#t canned the store and everything in it to the digital abyss.</td>
</tr>
<tr>
</table>

## Post Parameters
The post parameters and description of the post to your notification URL are as follows:

<table>
<tr>
<td><b>Parameter</b></td>
<td><b>Description</b></td>
</tr>
<tr>
<td>Details</td>
<td>This is a JSON array that includes the mobile ID, transaction ID, store ID, creation date for the message and subscriber's opt-in status.</td>
</tr>
<tr>
<td>message</td>
<td>The reason your request passed or failed.</td>
</tr>
<tr>
<tr>
<td>messageId</td>
<td>The ID of the message.</td>
</tr>
<tr>
<td>status</td>
<td>A pass or fail.  Any fail code for status means that the SMS API has blocked your message for one of the reasons above.</td>
</tr>
<tr>
<td>storeId</td>
<td>The store ID of the store you made the request with.</td>
</tr>
<tr>
<td>subscriberStatus</td>
<td>The opt-in status of the subscriber.</td>
</tr>
</table>

# Inbound Message Data

## How cloudwi.re Send Notifications
cloudwi.re makes HTTP requests to your application just like a regular web browser. By including parameters and values in its requests, cloudwi.re sends inbound messages, errors and job data to your application. You can configure the URL cloudwi.re uses to make its requests via your account portal or using the SMS API.

The SMS API will deliver notifications to your notification URL in multipart/form-data.  Additionally, cloudwi.re expects a 200 passed back to it in the header once your service has completed the handshake.  If you are responding to messaging dynamically and you notice latency, contact us.  We log the webhook start and end time and can help troubleshoot.

## For Those of You Developing Keyword Applications
If you are going to use keywords extensively, take note of a few things when working with the inbound messages.  This note only applies to a scenario where one store has multiple keywords  

If a subscriber opts-in to a store via an opt-in keyword, cloudwi.re will pass that keyword and keyword ID every time the subscriber sends the store a text,  except when the subscriber uses a responder keyword.  

That means if the subscriber sends in another opt-in keyword after opting-in, cloudwi.re will still tell the developer which keyword the subscriber originally opted-in on.  If you plan to house multiple opt-in keywords then you'll want to work your development around the message body parameter instead of the keyword parameter.

If you intend to dynamically respond to responder keywords, cloudwi.re will always pass the responder keyword ID for the keyword the subscriber sent in.  You'll want to capture the keyword and the keyword ID parameters in order to send your one-time response to the subscriber.  

We will eventually update the listener to better account for subscribers that may be using multiple keywords inside of one store.  

## Inbound Messages
Inbound messages from the mobile subscriber to the store are posted in real-time.  We will post any and all messages that belong to the store.  It will include MO SMS and MMS from your opted-in subscribers, opt-in and responder keywords and lastly, opt-out and help requests.

The following data is posted to your inbound message callback URL when a subscriber initiates a message from their device to your store.

Updates posted to the inbound message URL deliver in multipart/form-data. 

<table >
<tr>
<td><b>Parameter</b></td>
<td><b>Sample Value</b></td>
<td><b>Description</b></td>
</tr>
<tr>
<td>accountId</td>
<td>9923fefdb6d16a105c4708ad9b</td>
<td>Your account ID number.</td>
</tr>
<tr>
<td>accountName</td>
<td>Jim's Pizzeria Parlors</td>
<td>Your account name.</td>
</tr>
<tr>
<td>commChannel</td>
<td>+24411</td>
<td>If Applicable. The short/long code the subscriber is binded to the store with for 2-way guaranteed messaging.  This field will only be populated when the subscriber is opted-in and sending either opt-in, stop or help keywords or regular 2-way messaging.  Responder keywords do not look up the opt-in status of the subscriber and will not display a comm channel.</td>
</tr>
<tr>
<td>created</td>
<td>03-22-2016 12:31:43</td>
<td>If Applicable:  The very first date and time that the subscriber was opted-in to the store....even if they opt-out and opt back in.  MM/DD/YYYY H:M:S:MS Format.  All times are GMT.</td>
</tr>
<tr>
<td>from</td>
<td>+19993338888</td>
<td>The mobile phone number of the subscriber that sent the message.</td>
</tr>
<tr>
<td>fromCountry</td>
<td>US</td>
<td>If Applicable:  The mobile subscriber's country.  NOTE:  This does not reflect their current location.</td>
</tr>
<tr>
<td>fromState</td>
<td>CA</td>
<td>If Applicable:  The mobile subscriber's registered State.  NOTE:  This does not reflect their current location.</td>
</tr>
<tr>
<td>fromCity</td>
<td>Brisbane</td>
<td>If Applicable:  The mobile subscriber's Registered City.  NOTE:  This does not reflect their current location.</td>
</tr>
<tr>
<td>fromZip</td>
<td>94321</td>
<td>If Applicable:  The mobile subscriber's Registered Zip Code.  NOTE:  This does not reflect their current location.</td>
</tr>
<tr>
<td>keyword</td>
<td>PIZZA</td>
<td>If Applicable:  This field will populate the opt-in keyword that the subscriber first uses to opt-in.  It will be displayed for 2-way messaging and compliance keywords as well.  However, If a responder keyword is sent, it will display the keyword the subscriber utilized.</td>
</tr><tr>
<td>keywordId</td>
<td>432983498234a9823dd928398239823ad32c</td>
<td>If Applicable:  This will report the ID of responder keyword that is utilized.  If no responder keyword is present in the inbound message this body will report the opt-in keyword ID the subscriber used to opt-in....even if they opt-out and opt back in using a different opt-in keyword this data is stored as the very first opt-in keyword interaction with the subscriber.</td>
</tr>
<tr>
<td>keywordType</td>
<td>responder</td>
<td>If Applicable:  If a responder keyword is present the keyword type will be responder.  If the subscriber utilized an opt-in, stop or help keyword, it will be populated with opt-in.</td>
</tr>
<tr>
<td>mediaUrl</td>
<td>https:\/\/api.twilio.com\/2010-04-01\/Accounts\/ACff9c</td>
<td>If Applicable.  The media URL of the media the subscriber sent to the store.</td>
</tr>
<tr>
<td>messageBody</td>
<td>Pizza 123</td>
<td>If Applicable.  The inbound message body from the subscriber.</td>
</tr>
<tr>
<td>messageCharcount</td>
<td>9</td>
<td>If Applicable:  The character count of the message.  Blank if only an MMS is sent.</td>
</tr>
<tr>
<td>messageId</td>
<td>MM3923lke232323993988409349283981c239m</td>
<td>The unique message ID of the message.</td>
</tr>
<tr>
<td>numMedia</td>
<td>1</td>
<td>If Applicable. The number of media URLs.</b></td>
</tr>
<tr>
<td>numSegments</td>
<td>1</td>
<td>If Applicable.  The number of 160 character segments of the message.  Blank if only an MMS is sent.</b></td>
</tr>
<tr>
<td>optInAttempts</td>
<td>1</td>
<td>The number of times double opt-in has been attempted before the subscriber replied Yes to an opt-in request.</b></td>
</tr>
<tr>
<td>received</td>
<td>11/30/2016 04:50:15</td>
<td>The date and time the message was received.  MM/DD/YYYY H:M:S:MS Format.  All times are GMT.</td>
</tr>
<tr>
<td>score</td>
<td>0.78249</td>
<td>The message sentiment score on a scale of -1-1 provided by IBM Watson. +1 being the most positive.</b></td>
</tr>
<tr>
<td>shortCode</td>
<td>+345345</td>
<td>If Applicable.  For a responder keyword, this value will populate with the short code the subscriber sent the responder keyword on.  For opt-in keywords it will report the keyword the subscriber first used on their very first opt-in interaction with the store....even if they opt-out and opt back in using a different keyword this data is stored as the very first opt-in keyword interaction with the subscriber.</td>
</tr>
<tr>
<td>storeId</td>
<td>ca3121d16a10e24608ad9a</td>
<td>The store ID of the store the message is belongs to.</td>
</tr>
<tr>
<td>storeName</td>
<td>Jim's Pizza</td>
<td>The name of the store the message is belongs to.</td>
</tr>
<tr>
<td >subscriberStatus</td>
<td>opted-In</td>
<td>The subscriber's opt-in status, (Exp: opted-in, opted-out, pending or blank if there is no status)</td>
</tr>
<tr>
<td >type</td>
<td>Positive</td>
<td>The overall sentiment of the inbound message from the subscriber provided by IBM Watson.  Either positive, neutral or negative.</b></td>
</tr>
</table>

# Supported Media

### Accepted URLs
In order to send MMS on cloudwi.re, your URL must begin with http:// or https://.  URLs containing www. will be rejected by our aggregator.  Make sure you test your URLs internally before sending media to subscribers.

To send MMS on the cloudwi.re SMS API you will be passing a URL in the parameters where allowed.  If a media type, or incorrect URL is posted that is not in this list below, cloudwi.re will reject it.  For example, a typical mediaUrl you may pass to the SMS API would look something like:  http://cloudwi.re/image/1234.png

The cloudwi.re admin console will not host images for you.  You must host the images on your side.  There are plenty of <a href="http://tinypic.com/" target="_blank">free image hosting</a> options out there to upload your image and generate a URL to pass as mediaUrl to the SMS API.  

## Supported Media

The following types of content are fully supported by cloudwi.re. This content will be formatted by the carriers for delivery on destination devices.  Payloads up to 5 MB are accepted.  Keep in mind that the payload max remains 5 MB even if you include an SMS with your MMS.  Plan accordingly.  

 * image/jpeg
 * image/gif (Animate Gifs are supported)
 * image/png


## Accepted Media
The cloudwi.re SMS API will accept and attempt to deliver the following media formats.  However, this media is not reformatted for delivery.  Unfortunately, cloudwi.re has only seen message sizes of 455 KB for the media types below consistently get delivered on all four carriers.  It is not a very significant amount of size to get a point across.

We do hope that changes soon, but make sure you have a plan to test any audio/video on multiple carriers for delivery.  cloudwi.re maintains test devices on all of the big four carriers.  We are happy to help you test.  Just <a href="mailto:support@cloudwi.re?Subject=I%20Want%20To%20Send%20Some%20Funky%20MMS" target="_top">email us</a>!

 * video/mpeg
 * video/mp4
 * audio/mp4
 * audio/mpeg
 
# Testing Troubleshooting

## API Connection Issues
<ul>
<li>Your firewall ports can interfere with connectivity to the SMS API.  The API operates on port 443.  Make sure you can access that port number through your firewall.</li>
<li>You did not update your IP addresses in the security portion of the admin portal.  Tell cloudwi.re the IP addresses you'll be communicating with us from and we can be friends.</li>
<li>You get invalid key or store ID errors.  Make sure your key and store IDs are correct.  You can login to the portal to check them.  Don't hesitate to contact us if you can't figure it out at <a href="mailto:support@cloudwi.re">support@cloudwi.re</a> Postman is a wonderful resource to test authentication with.</li>
</ul>

#### Your Test or Subscriber's Number(s) Never Gets or Stops Getting Messages<br><br>

<ul>
<li>Some carriers, like Sprint have legacy plans that block standard rate short code messaging.  T-Mobile does this as well, but it is not as prevalent.  Try a friend’s number on another network and see if that clears your problem.  If your friend's phone works, call your provider or go to one their stores and request that you receive text messages from short codes.</li>
<li>Make sure you didn’t opt-out, get locked or are in pending status.  You can check this with <a href="https://cloudwire.gelato.io/docs/versions/427198918690866548/resources/subscriber-management/endpoints/list-subscriber-managements-8ad09376-df59-4871-a349-a193367f42c0">Get Subscriber Status</a> in the Reporting Resource.</li>
<li>The carriers monitor their networks very closely and constant opt-ins/outs of the same mobile phone number carries red flags and sometimes results in your number being locked down from receiving short code messages.  Try sending START to the short code you were communicating with your store on, for example, START to 24411.  If that doesn’t alleviate the issue contact us at <a href="mailto:support@cloudwi.re">support@cloudwi.re</a>.</li>
<li>The cloudwi.re SMS API only allows one mobile number to be opted-in to 13 stores.  Opt-out out of your test stores by replying STOP to the codes you are  binded to them with.  If you have forgotten all the codes you are binded to no big deal.  We can manually remove you from all stores.  Just hit us up at <a href="mailto:support@cloudwi.re?Subject=Clear%20My%20Number" target="_top">support@cloudwi.re</a></li>
<li>If there are no carrier issues and you did everything right, cloudwi.re has noted that sometimes a hard reset of the device or clearing some device memory will do the trick.</li>
</ul>   

#### Messages Don't Deliver to Any Test Device</u></b>

<ul>
<li>The most likely issue is that you are calling the cloudwi.re SMS API with a phone number that is not formatted properly.  Make sure you are calling the API with the country code and mobile number only.  Example:  '19995553333'</li>
</ul>

#### Your Webhook Does Not Receive cloudwi.re Posts

<ul>
<li>TTest internally for timeouts. If we receive errors we will notify you via the email address on file for each account and we'll queue up the webhooks. cloudwi.re provides an API call to retrieve message history if you need it.</li>
<li>Make sure you have whitelisted our IP addresses which you can find in the admin portal.</li>
<li>http://runscope.com is an excellent resource for checking and troubleshooting webhook health.  
<li>If problems persist, email us at <a href="mailto:support@cloudwi.re">support@cloudwi.re</a></li>
</ul>

#### Message Display Issues

Testing messages and how they display is an important part of your development process.  Some issues you may see below.  Some of them, due to different carrier transcription processes, can be super difficult to control.  Much of this is covered in our <a href="https://cloudwire.gelato.io/guides/carriers-behave-differently-read-it">carrier guide</a>.  
<ul>
<li>Sending special characters can have different effects on different carriers.  Sprint will be your primary culprit.  Tread carefully and make sure you test.  If you need assistance, we are an email away.</li>
<li>Removing HTTP://, HTTPS:// or www. from a URL when sending it will make the link unclickable on some devices when embedding them in an SMS.  If you are going to send URLs inside an SMS make sure you include the complete link.  Example:  Click here for your coupon!  https://cloudwi.re/coupon.  Sure, it doesn't look a pretty, but neither does subscriber frustration with having to cut and paste.</li>
<li>If your message is breaking into 2 or more separate messages, be careful with your character count.  Best practice is to limit your message to 160 characters or less.</li>
</ul>

#### Message Latency - Delivery Delays

This could be the result of several possibilities.  Don't panic.  It does happen once in a while and it is generally a specific carrier issue.  
<ul>
<li>Remember that cloudwi.re short codes are shared.  Although rare, peak usage can result in message latency in 1-to-1 messaging scenarios.</li>
<li>Further on the above, we are constricted by messages per second bandwidth.  If you are sending a campaign of 150k SMS or MMS and your number is last on the list, it's going to take a little bit for your message to hit your phone.</li>
<li>Most common, carriers queues do on occasion get backed up or stop working altogether.  Make sure you sign up for <a href="http://cloudwire.status.io/">cloudwi.re alerts</a> for this type of event.  And don't be afraid to contact <a href="mailto:support@cloudwi.re">support@cloudwi.re</a> if you think there is an outage of some sort.</li>
</ul>

#### I Get Messages From Multiple Short Codes.  

Yes, indeed you do.  Read more about that <a href="https://cloudwire.gelato.io/guides/the-store-concept" target="_blank">here</a>.  To amplify our bandwidth the cloudwi.re SMS API round robins your opt-ins across four short codes.  If you are a developer testing by constantly opting in and out this can be a tad confusing.  But remember that the subscriber is only going to interact with one unique short code when communicating with each store they've opted into.  If you are a developer and set-up more than one store, even if you use them for Dev, UAT and production, each one of those three stores you opt-in to will bind you to a different short or long code to communicate with those stores.  Perfectly normal!  

So no worries.  Grab a Red Bull and chill.  We've been doing this for eight years.  The mobile universe is pretty adaptive to replying to the received message.  We wouldn't have made it this long if they weren't.

#### A Note About Delivery Status
Reminder, don't exactly count on its accuracy.  We believe it's right about 95%  of the time.  For those developers that put high use testing environments in place you may experience this.  Simply report it to us and we'll give you every detail we can find.  But keep in mind that the carriers don't exactly respond to one-off requests as to why one or two people didn't get a text.  

That's because they are busy making funny commercials with chainsaws or magenta flashing seizure graphics.
received