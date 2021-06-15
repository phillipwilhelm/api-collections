<a href="http://www.sapphireims.com" ><img  src="https://www.sapphireims.com/wp-content/uploads/2017/03/Saphire-Logo-Web.png"  width="170px" alt="Sapphire Logo Web"></a>

<p> © COPYRIGHT Tecknodreams Software Consulting Pvt. Ltd.</p>

<p>Information in this user guide, including URLs and other
Internet Web site references, is subject to change without notice. Unless otherwise noted, the
companies, organizations, products, domain names, e-mail addresses, logos, people, places, and
events depicted in examples herein are fictitious. No association with any real company,
organization, product, domain name, e-mail address, logo, person, place, or event is intended or
should be inferred.
Complying with all applicable copyright laws is the responsibility of the user. Without limiting the
rights under copyright, no part of this user guide may be reproduced, stored in or introduced into a
retrieval system, or transmitted in any form or by any means (electronic, mechanical,
photocopying, recording, or otherwise), or for any purpose, without the express written permission
of Tecknodreams Software Consulting Pvt. Ltd. </p>


<h2 id="introduction">INTRODUCTION</h2>

SapphireIMS makes businesses agile through a modular and easy to implement suite of products, such as ITIL Service Desk, Enterprise Asset Management, Enterprise Service Management, Business Service Monitoring and Service Lifecycle Management. Our Healthcare Service Management solution is specifically designed for the needs of the healthcare industry.



<h3 id="what-is-the-bullhorn-rest-api">What is the SapphireIMS REST API?</h3>

<p>The SapphireIMS REST API gives Partners and Customers a simple yet powerful way to interact with the SapphireIMS system and thereby integrate SapphireIMS with other applications in the ecosystem. Because it uses HTTP requests, responses, and standard data structures, the REST API is accessible from many programming languages and applications that use the most current web technologies.</p>


<h3 id="what-is-postman">What is Postman?</h3>

<p>Postman is a tool which helps you build, test, and document APIs faster. Postman helps to create API clients in different languages. Download and Install the Postman application. Please refer the link for the Postman document <a href="https://learning.getpostman.com/docs/postman/launching_postman/installation_and_updates" alt="Post Man Document/">here!</a> We have created a bundle that includes all of the commonly used API calls with the REST API.  This is the first step in getting started with the SapphireIMS REST API.</p>

<h3 id="import-configuration-into-postman">Import Configuration into Postman</h3>

<p>You can import the configuration into Postman by clicking on the “Run In Postman” button located in the header of this document.</p>

<h3 id="setup-your-environment">Setup your Environment</h3>

<p>Now we are almost ready to get started. The last step is to setup your environment. From the environment drop down in the upper right of the application, select “Manage Environments.” As shown in the screenshot, you need to add the environment variables shown below to test.</p>

<p>key -   Authentication Key, Get the key details from SapphireIMS Support<p>
<p>token - Authentication token, Get the token details from SapphireIMS Support <p>
<p>int-log-id a unique id for each request   <p>
<p>url -  URL where the SapphireIMS application is deployed <p>

<p><img src="https://bullhorn.github.io/images/postman/PostmanManageEnvironment.png" alt="Enviornment variables" /></p>

<p>SapphireIMS Error Codes :  </br>

SUCCESS, "200" </br>
DUPLICATE_ENTITY, "501" </br>
ENTITY_DELETED, "502"</br>
DUPLICATE_USER, "404"</br>
UNAUTHORIZED, "403"</br>
INVALID_LOGIN, "405"</br>
USER_INACTIVE, "407"</br>
USER_LOCKED, "408"</br>
SESSION_EXPIRED, "409"</br>
INVALID_INPUT, "300"</br>
NO_SUCH_ENTITY, "301"</br>
NO_RESULT_FOUND, "302"</br>
SYS_ERROR, "500"</br>
VALIDATION, "303"</br>
THIRD_PARTY_SERVER_NOT_REACHABLE, "504"</br>
INVALID_TOKEN, "1004"</br>
AUTOMATION_SERVER_DOWN, "1005" </p>