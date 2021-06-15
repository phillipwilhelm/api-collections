# Retailer API
* [Product Methods](#ab643f2b-ad84-4828-9828-a659fb8dafd1)
* [Order Methods](#d5d48533-46cf-4d9e-8090-58676badbbbb)

# Partner API
* [Retailer Methods](#a1f96cff-a058-4851-be1e-53fd9ecbc4be)

# Doba API

*The Doba API allows you to utilize the Doba supply chain platform programmatically within your own application. The API includes functions to search or browse the Doba product catalog, obtain detailed product information, lookup shipping and handling charges, submit orders, fund orders, obtain shipment information for orders when they ship.*

----------

The API includes the following systems:

## Sandbox
(https://www.sandbox.doba.com)

A sandbox is a testing environment that isolates untested code changes and outright experimentation from the production environment. Sandbox environments protect production servers and their data from changes that could be damaging (regardless of the intent of the author of those changes) to a mission-critical system or which could simply be difficult to revert. Sandboxes replicate the functionality needed to test accurately the programs or other code under development.

***Notice***: Although we strive to keep the sandbox server available at all times, there may be times when it will not be accessible. If this is the case, please contact Doba.


## Product Methods
Allow for the retrieval of on-demand and up-to-the-minute product data from the Doba platform. These are available for use by both retailers and partners.

***Notice***: When downloading more than 10,000 products, we recommend using a private FTP Solution. Contact your Doba account representative to learn more. Downloading large data sets via the API can take long periods of time, and flat files are often easier to work with when dealing with large sets of data.

## Order Methods
Allow for the submittal of orders to the Doba platform as well as the retrieval of current order status and shipping/tracking data. These are available for use by both retailers and partners.

Orders submitted via the API can be funded through the API using several different payment methods.

Current order status can be called at any time through the use of the getOrders and getOrderDetail methods.


## Retailer Methods
Allow for the creation and manipulation of Doba member accounts. These are only available to partners. Retailers cannot use these methods

There are specific methods used to submit leads or new users to the Doba platform. If agreed to beforehand, revenue due to upgrades and subscription payments can be shared.

--------

## XML API URLs

When implementing the API using XML, you will POST your calls to the URL intended for the environment you are currently working in.

**Sandbox [development and testing]:**

* **retailer access** - https://sandbox.doba.com/api/20110301/xml_retailer_api.php
* **partner access** - https://sandbox.doba.com/api/20110301/xml_partner_api.php

**Live [After development and testing]:**

* **retailer access** - https://www.doba.com/api/20110301/xml_retailer_api.php
* **partner access** - https://www.doba.com/api/20110301/xml_partner_api.php

-------

## SOAP API URLs

**Sandbox [development and testing]:**

Product Methods:

* **retailer access** - https://sandbox.doba.com/soap/20110301/wsdl/ApiRetailerSearch.wsdl
* **partner access** - https://sandbox.doba.com/soap/20110301/wsdl/ApiPartnerSearch.wsdl

Order Methods:

* **retailer access** - https://sandbox.doba.com/soap/20110301/wsdl/ApiRetailerOrder.wsdl
* **partner access** - https://sandbox.doba.com/soap/20110301/wsdl/ApiPartnerOrder.wsdl

Retailer Methods:

* **retailer access** - Not applicable
* **partner access** - https://sandbox.doba.com/soap/20110301/wsdl/ApiPartnerRetailer.wsdl

**Live [After development and testing]:**

Product Methods:

* **retailer access** - https://legacy.doba.com/soap/20110301/wsdl/ApiRetailerSearch.wsdl
* **partner access** - https://legacy.doba.com/soap/20110301/wsdl/ApiPartnerSearch.wsdl

Order Methods:

* **retailer access** - https://legacy.doba.com/soap/20110301/wsdl/ApiRetailerOrder.wsdl
* **partner access** - https://legacy.doba.com/soap/20110301/wsdl/ApiPartnerOrder.wsdl
 
Retailer Methods:

* **retailer access** - Not applicable
* **partner access** - https://legacy.doba.com/soap/20110301/wsdl/ApiPartnerRetailer.wsdl

--------

# XML Response Outline
Each API request will return a response inside the <response> tag. The <action> tag will repeat the action requested.

The <outcome> tag will indicate whether the call succeeded or failed. If the call failed, it will provide additional information that will indicate the level of failure that has occurred.

The ENTITY information is provided to ensure that no special characters will cause problems while parsing the data. Your XML parsing system should use the ENTITY information to replace special characters throughout the response automatically.

<pre>
&lt;?xml version=&quot;1.0&quot;?&gt;
&lt;!DOCTYPE dce [
&lt;!ENTITY apos &quot;&amp;#39;&quot;&gt;
&lt;!ENTITY minus &quot;&amp;#45;&quot;&gt;
&lt;!ENTITY circ &quot;&amp;#94;&quot;&gt;
&lt;!ENTITY tilde &quot;&amp;#126;&quot;&gt;
&lt;!ENTITY Scaron &quot;&amp;#138;&quot;&gt;
&lt;!ENTITY lsaquo &quot;&amp;#139;&quot;&gt;
&lt;!ENTITY OElig &quot;&amp;#140;&quot;&gt;
&lt;!ENTITY lsquo &quot;&amp;#145;&quot;&gt;
&lt;!ENTITY rsquo &quot;&amp;#146;&quot;&gt;
&lt;!ENTITY ldquo &quot;&amp;#147;&quot;&gt;
&lt;!ENTITY rdquo &quot;&amp;#148;&quot;&gt;
&lt;!ENTITY bull &quot;&amp;#149;&quot;&gt;
&lt;!ENTITY ndash &quot;&amp;#150;&quot;&gt;
&lt;!ENTITY mdash &quot;&amp;#151;&quot;&gt;
&lt;!ENTITY trade &quot;&amp;#153;&quot;&gt;
&lt;!ENTITY scaron &quot;&amp;#154;&quot;&gt;
&lt;!ENTITY rsaquo &quot;&amp;#155;&quot;&gt;
&lt;!ENTITY oelig &quot;&amp;#156;&quot;&gt;
&lt;!ENTITY Yuml &quot;&amp;#159;&quot;&gt;
&lt;!ENTITY yuml &quot;&amp;#255;&quot;&gt;
&lt;!ENTITY fnof &quot;&amp;#402;&quot;&gt;
&lt;!ENTITY Alpha &quot;&amp;#913;&quot;&gt;
&lt;!ENTITY Beta &quot;&amp;#914;&quot;&gt;
&lt;!ENTITY Gamma &quot;&amp;#915;&quot;&gt;
&lt;!ENTITY Delta &quot;&amp;#916;&quot;&gt;
&lt;!ENTITY Epsilon &quot;&amp;#917;&quot;&gt;
&lt;!ENTITY Zeta &quot;&amp;#918;&quot;&gt;
&lt;!ENTITY Eta &quot;&amp;#919;&quot;&gt;
&lt;!ENTITY Theta &quot;&amp;#920;&quot;&gt;
&lt;!ENTITY Iota &quot;&amp;#921;&quot;&gt;
&lt;!ENTITY Kappa &quot;&amp;#922;&quot;&gt;
&lt;!ENTITY Lambda &quot;&amp;#923;&quot;&gt;
&lt;!ENTITY Mu &quot;&amp;#924;&quot;&gt;
&lt;!ENTITY Nu &quot;&amp;#925;&quot;&gt;
&lt;!ENTITY Xi &quot;&amp;#926;&quot;&gt;
&lt;!ENTITY Omicron &quot;&amp;#927;&quot;&gt;
&lt;!ENTITY Pi &quot;&amp;#928;&quot;&gt;
&lt;!ENTITY Rho &quot;&amp;#929;&quot;&gt;
&lt;!ENTITY Sigma &quot;&amp;#931;&quot;&gt;
&lt;!ENTITY Tau &quot;&amp;#932;&quot;&gt;
&lt;!ENTITY Upsilon &quot;&amp;#933;&quot;&gt;
&lt;!ENTITY Phi &quot;&amp;#934;&quot;&gt;
&lt;!ENTITY Chi &quot;&amp;#935;&quot;&gt;
&lt;!ENTITY Psi &quot;&amp;#936;&quot;&gt;
&lt;!ENTITY Omega &quot;&amp;#937;&quot;&gt;
&lt;!ENTITY alpha &quot;&amp;#945;&quot;&gt;
&lt;!ENTITY beta &quot;&amp;#946;&quot;&gt;
&lt;!ENTITY gamma &quot;&amp;#947;&quot;&gt;
&lt;!ENTITY delta &quot;&amp;#948;&quot;&gt;
&lt;!ENTITY epsilon &quot;&amp;#949;&quot;&gt;
&lt;!ENTITY zeta &quot;&amp;#950;&quot;&gt;
&lt;!ENTITY eta &quot;&amp;#951;&quot;&gt;
&lt;!ENTITY theta &quot;&amp;#952;&quot;&gt;
&lt;!ENTITY iota &quot;&amp;#953;&quot;&gt;
&lt;!ENTITY kappa &quot;&amp;#954;&quot;&gt;
&lt;!ENTITY lambda &quot;&amp;#955;&quot;&gt;
&lt;!ENTITY mu &quot;&amp;#956;&quot;&gt;
&lt;!ENTITY nu &quot;&amp;#957;&quot;&gt;
&lt;!ENTITY xi &quot;&amp;#958;&quot;&gt;
&lt;!ENTITY omicron &quot;&amp;#959;&quot;&gt;
&lt;!ENTITY pi &quot;&amp;#960;&quot;&gt;
&lt;!ENTITY rho &quot;&amp;#961;&quot;&gt;
&lt;!ENTITY sigmaf &quot;&amp;#962;&quot;&gt;
&lt;!ENTITY sigma &quot;&amp;#963;&quot;&gt;
&lt;!ENTITY tau &quot;&amp;#964;&quot;&gt;
&lt;!ENTITY upsilon &quot;&amp;#965;&quot;&gt;
&lt;!ENTITY phi &quot;&amp;#966;&quot;&gt;
&lt;!ENTITY chi &quot;&amp;#967;&quot;&gt;
&lt;!ENTITY psi &quot;&amp;#968;&quot;&gt;
&lt;!ENTITY omega &quot;&amp;#969;&quot;&gt;
&lt;!ENTITY thetasym &quot;&amp;#977;&quot;&gt;
&lt;!ENTITY upsih &quot;&amp;#978;&quot;&gt;
&lt;!ENTITY piv &quot;&amp;#982;&quot;&gt;
&lt;!ENTITY ensp &quot;&amp;#8194;&quot;&gt;
&lt;!ENTITY emsp &quot;&amp;#8195;&quot;&gt;
&lt;!ENTITY thinsp &quot;&amp;#8201;&quot;&gt;
&lt;!ENTITY zwnj &quot;&amp;#8204;&quot;&gt;
&lt;!ENTITY zwj &quot;&amp;#8205;&quot;&gt;
&lt;!ENTITY lrm &quot;&amp;#8206;&quot;&gt;
&lt;!ENTITY rlm &quot;&amp;#8207;&quot;&gt;
&lt;!ENTITY sbquo &quot;&amp;#8218;&quot;&gt;
&lt;!ENTITY bdquo &quot;&amp;#8222;&quot;&gt;
&lt;!ENTITY dagger &quot;&amp;#8224;&quot;&gt;
&lt;!ENTITY Dagger &quot;&amp;#8225;&quot;&gt;
&lt;!ENTITY hellip &quot;&amp;#8230;&quot;&gt;
&lt;!ENTITY permil &quot;&amp;#8240;&quot;&gt;
&lt;!ENTITY prime &quot;&amp;#8242;&quot;&gt;
&lt;!ENTITY Prime &quot;&amp;#8243;&quot;&gt;
&lt;!ENTITY oline &quot;&amp;#8254;&quot;&gt;
&lt;!ENTITY frasl &quot;&amp;#8260;&quot;&gt;
&lt;!ENTITY euro &quot;&amp;#8364;&quot;&gt;
&lt;!ENTITY image &quot;&amp;#8465;&quot;&gt;
&lt;!ENTITY weierp &quot;&amp;#8472;&quot;&gt;
&lt;!ENTITY real &quot;&amp;#8476;&quot;&gt;
&lt;!ENTITY alefsym &quot;&amp;#8501;&quot;&gt;
&lt;!ENTITY larr &quot;&amp;#8592;&quot;&gt;
&lt;!ENTITY uarr &quot;&amp;#8593;&quot;&gt;
&lt;!ENTITY rarr &quot;&amp;#8594;&quot;&gt;
&lt;!ENTITY darr &quot;&amp;#8595;&quot;&gt;
&lt;!ENTITY harr &quot;&amp;#8596;&quot;&gt;
&lt;!ENTITY crarr &quot;&amp;#8629;&quot;&gt;
&lt;!ENTITY lArr &quot;&amp;#8656;&quot;&gt;
&lt;!ENTITY uArr &quot;&amp;#8657;&quot;&gt;
&lt;!ENTITY rArr &quot;&amp;#8658;&quot;&gt;
&lt;!ENTITY dArr &quot;&amp;#8659;&quot;&gt;
&lt;!ENTITY hArr &quot;&amp;#8660;&quot;&gt;
&lt;!ENTITY forall &quot;&amp;#8704;&quot;&gt;
&lt;!ENTITY part &quot;&amp;#8706;&quot;&gt;
&lt;!ENTITY exist &quot;&amp;#8707;&quot;&gt;
&lt;!ENTITY empty &quot;&amp;#8709;&quot;&gt;
&lt;!ENTITY nabla &quot;&amp;#8711;&quot;&gt;
&lt;!ENTITY isin &quot;&amp;#8712;&quot;&gt;
&lt;!ENTITY notin &quot;&amp;#8713;&quot;&gt;
&lt;!ENTITY ni &quot;&amp;#8715;&quot;&gt;
&lt;!ENTITY prod &quot;&amp;#8719;&quot;&gt;
&lt;!ENTITY sum &quot;&amp;#8721;&quot;&gt;
&lt;!ENTITY lowast &quot;&amp;#8727;&quot;&gt;
&lt;!ENTITY radic &quot;&amp;#8730;&quot;&gt;
&lt;!ENTITY prop &quot;&amp;#8733;&quot;&gt;
&lt;!ENTITY infin &quot;&amp;#8734;&quot;&gt;
&lt;!ENTITY ang &quot;&amp;#8736;&quot;&gt;
&lt;!ENTITY and &quot;&amp;#8743;&quot;&gt;
&lt;!ENTITY or &quot;&amp;#8744;&quot;&gt;
&lt;!ENTITY cap &quot;&amp;#8745;&quot;&gt;
&lt;!ENTITY cup &quot;&amp;#8746;&quot;&gt;
&lt;!ENTITY int &quot;&amp;#8747;&quot;&gt;
&lt;!ENTITY there4 &quot;&amp;#8756;&quot;&gt;
&lt;!ENTITY sim &quot;&amp;#8764;&quot;&gt;
&lt;!ENTITY cong &quot;&amp;#8773;&quot;&gt;
&lt;!ENTITY asymp &quot;&amp;#8776;&quot;&gt;
&lt;!ENTITY ne &quot;&amp;#8800;&quot;&gt;
&lt;!ENTITY equiv &quot;&amp;#8801;&quot;&gt;
&lt;!ENTITY le &quot;&amp;#8804;&quot;&gt;
&lt;!ENTITY ge &quot;&amp;#8805;&quot;&gt;
&lt;!ENTITY sub &quot;&amp;#8834;&quot;&gt;
&lt;!ENTITY sup &quot;&amp;#8835;&quot;&gt;
&lt;!ENTITY nsub &quot;&amp;#8836;&quot;&gt;
&lt;!ENTITY sube &quot;&amp;#8838;&quot;&gt;
&lt;!ENTITY supe &quot;&amp;#8839;&quot;&gt;
&lt;!ENTITY oplus &quot;&amp;#8853;&quot;&gt;
&lt;!ENTITY otimes &quot;&amp;#8855;&quot;&gt;
&lt;!ENTITY perp &quot;&amp;#8869;&quot;&gt;
&lt;!ENTITY sdot &quot;&amp;#8901;&quot;&gt;
&lt;!ENTITY lceil &quot;&amp;#8968;&quot;&gt;
&lt;!ENTITY rceil &quot;&amp;#8969;&quot;&gt;
&lt;!ENTITY lfloor &quot;&amp;#8970;&quot;&gt;
&lt;!ENTITY rfloor &quot;&amp;#8971;&quot;&gt;
&lt;!ENTITY lang &quot;&amp;#9001;&quot;&gt;
&lt;!ENTITY rang &quot;&amp;#9002;&quot;&gt;
&lt;!ENTITY loz &quot;&amp;#9674;&quot;&gt;
&lt;!ENTITY spades &quot;&amp;#9824;&quot;&gt;
&lt;!ENTITY clubs &quot;&amp;#9827;&quot;&gt;
&lt;!ENTITY hearts &quot;&amp;#9829;&quot;&gt;
&lt;!ENTITY diams &quot;&amp;#9830;&quot;&gt;
&lt;!ENTITY nbsp &quot;&amp;#160;&quot;&gt;
&lt;!ENTITY iexcl &quot;&amp;#161;&quot;&gt;
&lt;!ENTITY cent &quot;&amp;#162;&quot;&gt;
&lt;!ENTITY pound &quot;&amp;#163;&quot;&gt;
&lt;!ENTITY curren &quot;&amp;#164;&quot;&gt;
&lt;!ENTITY yen &quot;&amp;#165;&quot;&gt;
&lt;!ENTITY brvbar &quot;&amp;#166;&quot;&gt;
&lt;!ENTITY sect &quot;&amp;#167;&quot;&gt;
&lt;!ENTITY uml &quot;&amp;#168;&quot;&gt;
&lt;!ENTITY copy &quot;&amp;#169;&quot;&gt;
&lt;!ENTITY ordf &quot;&amp;#170;&quot;&gt;
&lt;!ENTITY laquo &quot;&amp;#171;&quot;&gt;
&lt;!ENTITY not &quot;&amp;#172;&quot;&gt;
&lt;!ENTITY shy &quot;&amp;#173;&quot;&gt;
&lt;!ENTITY reg &quot;&amp;#174;&quot;&gt;
&lt;!ENTITY macr &quot;&amp;#175;&quot;&gt;
&lt;!ENTITY deg &quot;&amp;#176;&quot;&gt;
&lt;!ENTITY plusmn &quot;&amp;#177;&quot;&gt;
&lt;!ENTITY sup2 &quot;&amp;#178;&quot;&gt;
&lt;!ENTITY sup3 &quot;&amp;#179;&quot;&gt;
&lt;!ENTITY acute &quot;&amp;#180;&quot;&gt;
&lt;!ENTITY micro &quot;&amp;#181;&quot;&gt;
&lt;!ENTITY para &quot;&amp;#182;&quot;&gt;
&lt;!ENTITY middot &quot;&amp;#183;&quot;&gt;
&lt;!ENTITY cedil &quot;&amp;#184;&quot;&gt;
&lt;!ENTITY sup1 &quot;&amp;#185;&quot;&gt;
&lt;!ENTITY ordm &quot;&amp;#186;&quot;&gt;
&lt;!ENTITY raquo &quot;&amp;#187;&quot;&gt;
&lt;!ENTITY frac14 &quot;&amp;#188;&quot;&gt;
&lt;!ENTITY frac12 &quot;&amp;#189;&quot;&gt;
&lt;!ENTITY frac34 &quot;&amp;#190;&quot;&gt;
&lt;!ENTITY iquest &quot;&amp;#191;&quot;&gt;
&lt;!ENTITY Agrave &quot;&amp;#192;&quot;&gt;
&lt;!ENTITY Aacute &quot;&amp;#193;&quot;&gt;
&lt;!ENTITY Acirc &quot;&amp;#194;&quot;&gt;
&lt;!ENTITY Atilde &quot;&amp;#195;&quot;&gt;
&lt;!ENTITY Auml &quot;&amp;#196;&quot;&gt;
&lt;!ENTITY Aring &quot;&amp;#197;&quot;&gt;
&lt;!ENTITY AElig &quot;&amp;#198;&quot;&gt;
&lt;!ENTITY Ccedil &quot;&amp;#199;&quot;&gt;
&lt;!ENTITY Egrave &quot;&amp;#200;&quot;&gt;
&lt;!ENTITY Eacute &quot;&amp;#201;&quot;&gt;
&lt;!ENTITY Ecirc &quot;&amp;#202;&quot;&gt;
&lt;!ENTITY Euml &quot;&amp;#203;&quot;&gt;
&lt;!ENTITY Igrave &quot;&amp;#204;&quot;&gt;
&lt;!ENTITY Iacute &quot;&amp;#205;&quot;&gt;
&lt;!ENTITY Icirc &quot;&amp;#206;&quot;&gt;
&lt;!ENTITY Iuml &quot;&amp;#207;&quot;&gt;
&lt;!ENTITY ETH &quot;&amp;#208;&quot;&gt;
&lt;!ENTITY Ntilde &quot;&amp;#209;&quot;&gt;
&lt;!ENTITY Ograve &quot;&amp;#210;&quot;&gt;
&lt;!ENTITY Oacute &quot;&amp;#211;&quot;&gt;
&lt;!ENTITY Ocirc &quot;&amp;#212;&quot;&gt;
&lt;!ENTITY Otilde &quot;&amp;#213;&quot;&gt;
&lt;!ENTITY Ouml &quot;&amp;#214;&quot;&gt;
&lt;!ENTITY times &quot;&amp;#215;&quot;&gt;
&lt;!ENTITY Oslash &quot;&amp;#216;&quot;&gt;
&lt;!ENTITY Ugrave &quot;&amp;#217;&quot;&gt;
&lt;!ENTITY Uacute &quot;&amp;#218;&quot;&gt;
&lt;!ENTITY Ucirc &quot;&amp;#219;&quot;&gt;
&lt;!ENTITY Uuml &quot;&amp;#220;&quot;&gt;
&lt;!ENTITY Yacute &quot;&amp;#221;&quot;&gt;
&lt;!ENTITY THORN &quot;&amp;#222;&quot;&gt;
&lt;!ENTITY szlig &quot;&amp;#223;&quot;&gt;
&lt;!ENTITY agrave &quot;&amp;#224;&quot;&gt;
&lt;!ENTITY aacute &quot;&amp;#225;&quot;&gt;
&lt;!ENTITY acirc &quot;&amp;#226;&quot;&gt;
&lt;!ENTITY atilde &quot;&amp;#227;&quot;&gt;
&lt;!ENTITY auml &quot;&amp;#228;&quot;&gt;
&lt;!ENTITY aring &quot;&amp;#229;&quot;&gt;
&lt;!ENTITY aelig &quot;&amp;#230;&quot;&gt;
&lt;!ENTITY ccedil &quot;&amp;#231;&quot;&gt;
&lt;!ENTITY egrave &quot;&amp;#232;&quot;&gt;
&lt;!ENTITY eacute &quot;&amp;#233;&quot;&gt;
&lt;!ENTITY ecirc &quot;&amp;#234;&quot;&gt;
&lt;!ENTITY euml &quot;&amp;#235;&quot;&gt;
&lt;!ENTITY igrave &quot;&amp;#236;&quot;&gt;
&lt;!ENTITY iacute &quot;&amp;#237;&quot;&gt;
&lt;!ENTITY icirc &quot;&amp;#238;&quot;&gt;
&lt;!ENTITY iuml &quot;&amp;#239;&quot;&gt;
&lt;!ENTITY eth &quot;&amp;#240;&quot;&gt;
&lt;!ENTITY ntilde &quot;&amp;#241;&quot;&gt;
&lt;!ENTITY ograve &quot;&amp;#242;&quot;&gt;
&lt;!ENTITY oacute &quot;&amp;#243;&quot;&gt;
&lt;!ENTITY ocirc &quot;&amp;#244;&quot;&gt;
&lt;!ENTITY otilde &quot;&amp;#245;&quot;&gt;
&lt;!ENTITY ouml &quot;&amp;#246;&quot;&gt;
&lt;!ENTITY divide &quot;&amp;#247;&quot;&gt;
&lt;!ENTITY oslash &quot;&amp;#248;&quot;&gt;
&lt;!ENTITY ugrave &quot;&amp;#249;&quot;&gt;
&lt;!ENTITY uacute &quot;&amp;#250;&quot;&gt;
&lt;!ENTITY ucirc &quot;&amp;#251;&quot;&gt;
&lt;!ENTITY uuml &quot;&amp;#252;&quot;&gt;
&lt;!ENTITY yacute &quot;&amp;#253;&quot;&gt;
&lt;!ENTITY thorn &quot;&amp;#254;&quot;&gt;
&lt;!ENTITY lt &quot;&amp;lt;&quot;&gt;
&lt;!ENTITY gt &quot;&amp;gt;&quot;&gt;
&lt;!ENTITY amp &quot;&amp;amp;&quot;&gt;
]&gt;
&lt;dce&gt;
 &lt;response&gt;
  &lt;outcome&gt;&lt;!-- 'success', 'failure'&nbsp;: level 3, 'api_error'&nbsp;: level 2, 'system_error'&nbsp;: level 1 --&gt;&lt;/outcome&gt;
  &lt;!-- if the outcome is not 'success' then the section below will contain error information --&gt;
  &lt;errors&gt;
   &lt;error&gt;
    &lt;/code&gt;
    &lt;/description&gt;
   &lt;/error&gt;
  &lt;/errors&gt;
  &lt;!-- response data specific to the request made --&gt;
 &lt;/response&gt;
&lt;/dce&gt;
</pre>


---------

# Failure Codes
Provides specific information regarding the failure of any given API call.

Because there are several layers at which an API call can fail, the API breaks the failures into varying code levels which are explained below.


### Level 1 = Fatal System Error, contact Doba
There was a system error and the request was unable to be processed. The call format and/or authentication may be OK, but the system was not able to process the request properly or there was a server or communication error. Typically, these calls should be resubmitted after the cause of the error has been resolved.

It is inevitable that this error level will be provided at some point in your integrations life-time. Although Doba strives for 100% uptime, it is not always possible. Doba monitors the systems responsible for keeping the API available at all times and will be notified of any problems. If you feel that Doba is taking an unreasonable amount of time to resolve the errors, please contact us.

### Level 2 = Syntax Error
There was a problem with request format.

The system is attempting to process your request, but there is a problem with the API call's XML format or the syntax of the action you are attempting to submit. Please review this documentation thoroughly to ensure that your calls are properly formatted. Please review your code and the syntax of the action you are attempting to ensure that all required sections of the call are accounted for. If this error persists, please contact Doba where your call can be reviewed and possible solution(s) can be provided.

### Level 3 = Data Error
There was a problem with the authentication.

Either your username or password is incorrect or your account is not currently active or it does not have the appropriate permissions assigned. If you are unable to resolve this error on your own, please contact Doba to find out if your account has been configured properly.

 

# Failure Code List



| Error    | Explanation |
| -------- | -------- |
|200		|Invalid action|
|201		|Permission denied|
|2011	|Permission denied no resource access|
|2012	|Permission denied neither partner nor retailer|
|2013	|Permission denied invalid retailer action|
|2014	|Permission denied invalid action|
|2015	|Permission denied insufficient permissions|
|2016	|Permission denied invalid credentials|
|2017	|Permission denied missing credentials|
|202		|Missing syntax|
|203		|Invalid xml|
|204		|Call requires https|
|300		|Non existent retailer|
|3001	|Retailer not expired|
|3002	|Retailer missing access sub|
|301		|Missing email|
|3010	|Email or phone required|
|302		|Missing firstname|
|303		|Missing lastname|
|304		|Missing phone|
|305		|Missing billing street|
|306		|Missing billing city|
|307		|Missing billing state|
|308		|Missing billing postal|
|309		|Missing billing country|
|310		|Missing creditcard number|
|311		|Missing creditcard expiration|
|312		|Missing username|
|313		|Missing api code|
|314		|Missing frequency|
|315		|Missing billing responsibility|
|316		|Missing trial|
|317		|Missing subscription action|
|318		|Missing retailer id|
|319		|Missing item id|
|320		|Missing quantity|
|321		|Missing shipping state|
|322		|Missing shipping postal|
|3220	|Invalid shipping postal|
|3221	|Shipping postal not allowed|
|3222	|Invalid billing postal|
|323		|Missing shipping country|
|324		|Missing order items|
|325		|Missing shipping city|
|326		|Missing shipping street|
|3260	|'Shipping street' longer than 25 characters|
|327		|Missing shipping firstname|
|328		|Missing shipping lastname|
|329		|Missing order id|
|330		|Missing fund method|
|331		|Missing payment account id|
|332		|Missing billing name|
|333		|Missing cvv2|
|334		|Missing orderlist item info|
|335		|Missing order status|
|336		|Missing orderlist items|
|337		|Missing billing lastname|
|338		|Missing billing firstname|
|339		|Missing creditcard expiration year|
|340		|Missing creditcard expiration month|
|341		|Missing Inventory List id|
|342		|Inventory List user mismatch|
|343		|Inventory List invalid|
|3430	|Folder invalid|
|344		|Could not save Inventory List|
|3440	|Max Inventory Lists reached|
|3441	|Duplicate Inventory List name|
|345		|Could not delete Inventory List|
|3450	|Could not add items|
|34501	|Items not available|
|346		|Missing saved search id|
|347		|Saved search user mismatch|
|348		|Saved search invalid|
|349		|Could not save search|
|3490	|Max saved searches reached|
|3491	|Duplicate saved search name|
|350		|Could not delete saved search|
|3501	|Old saved search|
|3502	|Duplicate customization profile name|
|3503	|Could not load customization profile|
|3504	|Customization profile not allowed|
|3505	|Could not delete customization profile|
|3506	|Could not rename customization profile|
|3507	|Empty customization profile name|
|3508	|Could not remove customization data from item|
|3509	|Missing customization profile id|
|351		|Order not specified|
|352		|Missing ip address|
|353		|Order not available to user|
|354		|Shipping address missing|
|355		|No items in cart|
|356		|Cannot cancel supplier order|
|357		|Missing cancellation reason|
|358		|No decisions submitted|
|359		|No decisions exist|
|360		|Invalid email|
|361		|Invalid phone|
|362		|Invalid creditcard number|
|363		|Invalid subscription action|
|364		|Invalid shipping state|
|365		|Invalid shipping country|
|366		|No action taken|
|367		|Invalid ip address|
|368		|Invalid username|
|369		|Username already exists|
|370		|Supplier order unavailable|
|371		|Missing rma reason|
|372		|Missing rma type|
|373		|Missing rma items|
|374		|Missing rma id|
|3740	|Missing shipment date|
|3741	|Invalid shipment date|
|3742	|Missing carrier|
|3743	|missing tracking|
|3744	|Invalid parcel count|
|3745	|Could not save tracking|
|375		|Missing warehouse folder path|
|3750001|Failed to copy folder|
|376		|Failed to save path|
|377		|Failed to delete folder|
|378		|Missing warehouse folder id|
|3780	|Push request id|
|379		|Failed to retrieve folders|
|380		|Permission to retailer denied|
|381		|Missing items|
|382		|Missing folder name|
|383		|Failed to add items to folder|
|3830	|Failed to add items to push request|
|3831	|Folder item limit reached|
|3830001|Failed to copy items to folder|
|384		|Failed to delete items from foler|
|385		|Failed to rename folder|
|3850	|Folder name already exists|
|386		|Invalid retailer id|
|3860	|Invalid from date|
|3861	|Invalid to date|
|387		|Invalid billing country|
|390		|Call limit reached|
|400		|Unavailable order item|
|4001	|Invalid order item|
|4002	|Duplicate order item|
|401		|Inaccessible order item|
|402		|Unavailable order|
|403		|Invalid order|
|404		|Invalid payment account|
|405		|Invalid subscription|
|406		|Invalid frequency|
|407		|Invalid billing responsibility|
|408		|Invalid order id|
|4080	|Invalid order group id|
|409		|Invalid order status|
|410		|Invalid order po number|
|411		|Cannot mix directrelation orders|
|4110	|Cannot group specified orders|
|4111	|Cannot ungroup specified orders|
|412		|Invalid export|
|413		|Missing export|
|416		|Missing export name|
|417		|Missing transform commands|
|418		|Invalid transform commands|
|419		|Missing records|
|420		|Missing url tag|
|421		|Invalid url tag|
|422		|Duplicate url tag|
|423		|Missing folder id|
|4230	|Missing search id|
|4231	|Missing source type|
|4232	|INvalid search id|
|424		|Invalid folder id|
|425		|Invalid changes since time|
|426		|Invalis changes since secs|
|427		|Missing transform|
|428		|Missing transform id|
|429		|Invalid transform id|
|430		|Missing transform name|
|431		|Missing transform format|
|432		|Invalid transform format|
|433		|Missing transform format parameters|
|434		|Invalid transform format parameters|
|435		|Invalid transform criteria|
|436		|Invalid transform scope|
|437		|Transform edit permission|
|438		|Could not load export|
|439		|Failed to run export|
|440		|Could not run export transform|
|441		|Failed to add export transform|
|442		|Failed to edit export transform|
|443		|Failed to delete export transform|
|444		|Failed to create product export|
|445		|Failed to edit product export|
|446		|Failed to delete product export|
|447		|Unavailable export|
|448		|Unavailable transform|
|500		|Failed to save order|
|501		|Failed to fund order|
|502		|Payment failed|
|503		|Failed to save payment|
|510		|Product not found|
|520		|Product id required|
|521		|Invalid status trigger|
|522		|Item id required|
|523		|Profile id required|
|530		|Trigger required|
|531		|Invalid status trigger|
|532		|Frequency required|
|534		|Frequency time required|
|535		|Invalid frequency time|
|536		|Unable to set folder preferences|
|537		|Unable to remove folder preferences|

--------

# Limits

Doba limits the number of *product* API calls per minute for each retailer account. For any given minute only 100 API calls will be allowed, any incoming connections will be rejected after the limit has been reached. To ensure that the limit is never reached, all API calls should be batched when possible. *Requesting details for one single product should be an exception rather than the rule.*

***There are no limits on Order API calls.**

--------

# Order Lifecycle
A Doba order will normally progress through the following four primary stages. These four stages are also the core statuses for the Doba order life cycle.

1. Payment Pending
2. Funded
3. Processing
4. Shipped

Understanding the order life cycle is important when building an application which includes Doba order integration.

You will notice that the "Awaiting Review" status is encountered during the course of some orders. This is a fraud prevention related step where the Doba order management team reviews orders and payments which exceed a risk threshold. No action is required by integration partners to progress orders through this step. A Doba support representative may contact the client in the process of reviewing orders.

At any point in the order process an order may be placed in a "hold" or "cancelled" status. The "hold" status is used when manual intervention is required during order processing. Examples of scenarios for held orders include shipping address correction. Both the "shipped" and "cancelled" status are considered terminal statuses.

 

## Order Statuses
It's important to understand the structure of an order to understand the different statuses that may be encountered through the order lifecycle.

A Doba order is broken into three levels. The highest level encompases the entire order, including the totals for all items, shipping, drop-ship fees, etc.

The second level contains all of the individual supplier orders, or orders broken into groups of items that come from the same supplier. Each supplier order will have its own status.

Because there can be multiple supplier orders in one order, the top-level order status will sometimes be "Various". This will happen if the suppler order status' differ from each another. If all supplier order status' are the same, the order status will be identical to the supplier order status'.

The scenerios below will help explain how different status' are represented:

### Order 1

	Order Status = Completed
	Supplier Order Status = Completed

### Order 2

	Order Status = Completed
	Supplier Order 1 Status = Completed
	Supplier Order 2 Status = Completed
	Supplier Order 3 Status = Completed

### Order 3

	Order Status = Various
	Supplier Order 1 Status = Completed
	Supplier Order 2 Status = Shipment Pending
	Supplier Order 3 Status = Completed

### Order 4
	
	Order Status = Cancelled
	Supplier Order 1 Status = Cancelled
	Supplier Order 2 Status = Cancelled
	Supplier Order 3 Status = Cancelled

### Order 5

	Order Status = Cancelled
	Supplier Order Status = Cancelled

The last level is item status which has its own set of statuses.

# Supplier Order Statuses
The full range of order lifecycle statuses are explained in the following table.

| STATUS	 | DESCRIPTION |
| ---------- | ----------- |
| Error - Contact Support	| The order is in an erroneous state and is being investigated by a Doba fulfillment specialist. |
| Awaiting Payment	| Customer must submit payment for the order to continue; initiated PayPal payment may be outstanding. |
| Funded	| The order has been funded. It is being processed by the Doba platform and will be deleivered to the supplier for fulfillment if no problems are found. |
| Shipped	| Shipment information has been received from the supplier and the order is en-route or received. |
| Payment Declined	| Authorized payment failed to settle. |
| Processing	| The Doba order engine is processing the order. This status is fleeting and will normally not be encountered by integrated systems. |
| Hold - Input Needed	| Retailer input is needed for the order to be processed; customer is notified by e-mail and can provide input by logging into the site. |
| Shipment Pending	| The order has been sent to the supplier and is being fulfilled; Doba is waiting for supplier response and a shipment notice is expected. |
| Awaiting Payment Confirmation	 |This normally only occurs during an eCheck transaction through PayPal, where Doba is notified of the payment but it has not yet cleared. |
| Awaiting Supplier Cancel	| The customer has requested cancellation and Doba is initiating the cancellation process with the supplier. |
| Cancelled	| The order is cancelled and will not be fulfilled. |
| Fraudulent Order	| The order was aborted and deemed to be fraudulent. |
| Returned	| The product(s) have been returned to the supplier and return receipt verified. |
| Completed	| The order completed normally. |
| Awaiting Supplier Acceptance	| Some suppliers use an asynchronous acknowledgement. In this state the order has been submitted but not acknowledged. |

---------

# Line Item Statuses
In addition to better overall order tracking and statuses the API also exposes line item statuses for each item in an order.

| STATUS	| DESCRIPTION |
| --------- | ----------- |
| Pending	| The item is waiting to be sent to the supplier. |
| Processing	| The DOBA order engine is processing the order. This status is fleeting and will normally not be encountered by integrated systems. |
| Scheduled	| The item has not yet been accepted by the supplier as part of an order, but the order is on back order with Doba. i.e. Doba is waiting for new inventory to re-send the item to the supplier. |
| Shipment Pending	| The item has been sent to the supplier. |
| Shipped	| The item is on route to the end consumer. |
| Partial	| Some of the quantity have shipped, others are pending shipment or possible cancellation. |
| Cancelled	| The item has been cancelled and removed from the order. |
| Returned	| The item has been returned to the supplier. |
| Discontinued	| The item has been discontinued and removed from the order. |
| Waiting	| The item is waiting for the supplier to update its status. |


-------

# Order Lifecycle Integration Workflow
Typically, when integrating the Order API into your application, you will want to follow the outline below as a basic workflow.

1. Gather all item_id's and call the orderLookup function making sure to deal with any out-of-stock items or items that may not be currently available.
2. Display the totals found in the orderLookup function and wait for the end-user to submit the final order.
3. Create the order using the createOrder API method. You may wish to immediately fund the order using the fundOrder method after creating the order. You could also do this at a separate time.
4. Check on the order status at the time of your choice using the getOrders or the getOrderDetail methods.