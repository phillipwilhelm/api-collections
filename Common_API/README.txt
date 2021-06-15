# Purpose
There are multiple Common APIs available to manage New Hires as well as master data across OVA portals. 

To call any of these APIs, client needs to send Customer specific GUID, and share the credentials of HR Admin or Account Manager.

Client application's can access these Common API's in one of the below approaches:
<br>
1. By using postman app. Download this postman app here <a href="https://www.postman.com/downloads/" target="_blank"> Postman App </a> <br>
2. By Calling the individual Common API's through their web interface (check the sample code section below. It provides sample code for calling common APIs using Java).
<br><br>

You can test these Common API's by clicking on <i>Run in postman</i> button accessible on the top right corner of each related API documentation page.

# Authentication

<li>Before calling any API, first make an API call to 'Get Token' common API. This is to get access token as per Unique Customer GUID. 
<br>
<br>
<li>The Common API will only respond to secured communication done over HTTPS. HTTP requests will be sent a <code>301</code> redirect to corresponding HTTPS resources.
<br>
<br>
<li>Response to every request is sent in **JSON format**. In case the API request results in an error, it is represented by an <code>"error": {}</code> key in the JSON response.
<br>
<br>
<li>The request method determines the nature of action you intend to perform. A request made using the <code>GET</code> method implies that you want to fetch something from Postman, and <code>POST</code> implies you want to save something new to Postman.
<br>
<br>
<li>The API calls will respond with appropriate **HTTP status codes** for all requests. Within Postman Client, when a response is received, the status code is highlighted and is accompanied by a help text that indicates the possible meaning of the response code. A <code>200 OK</code> indicates all went well, while <code>4XX</code> or <code>5XX</code> response codes indicate an error from the requesting client or our API servers respectively.

<br>
<br>

# Sample Code
This sample code is useful for calling common APIs from client web applications.

It calls Get Token API first. After this it calls Add Source API.

It is mandatory to call Get Token API for validating and get authorized before calling any of the common APIs.

<pre>import java.io.FileInputStream;  
import java.io.FileOutputStream;  
import java.io.IOException;  
import java.util.Iterator;

import org.apache.commons.httpclient.HttpClient;
import org.apache.commons.httpclient.MultiThreadedHttpConnectionManager;
import org.apache.commons.httpclient.NameValuePair;
import org.apache.commons.httpclient.methods.GetMethod;
import org.apache.commons.httpclient.methods.PostMethod;
import org.codehaus.jettison.json.JSONObject;

import java.io.IOException;  
import java.io.InputStream;  
import java.util.Iterator;  
import java.util.ArrayList;



public class  AppTest
{
	public static void main(String[] args) 
	{
		HttpClient con;
		MultiThreadedHttpConnectionManager connectionManager = 	new MultiThreadedHttpConnectionManager();
				connectionManager.getParams().setDefaultMaxConnectionsPerHost(20000);  
				connectionManager.getParams().setMaxTotalConnections(20000);  
				con = new HttpClient(connectionManager); 
								
				PostMethod method = null;
				GetMethod gmethod = null;
				NameValuePair[] pairs =null;

				String token="",src="";


				JSONObject obj= null;

				// get token

				obj = new JSONObject();

				method = new PostMethod("http://192.168.1.198:8080/CommonApis/gettoken");
				obj.put("emailId","john@ova.work");
				obj.put("password","john@123");
				obj.put("guId","c5144c6a-af00-46b1-9d46-495811e7c55b");
				method.setRequestHeader("Content-Type","application/json");
				
				method.setRequestBody(obj.toString());
				con.executeMethod(method);
				token = method.getResponseHeader("ova-auth-token").toString();
				src = method.getResponseBodyAsString();
System.out.println("token --> " +token);
			// post method

				if(token.indexOf(":") != -1) token = token.substring(token.indexOf(":")+1).trim();
				method = new PostMethod("http://192.168.1.197:8900/CommonApis/addsource");  // url
				method.setRequestHeader("Content-Type","application/json");
				method.setRequestHeader("ova-auth-token",token); // token

				obj = new JSONObject();
				obj.put("sourcename","Monster");
				obj.put("description","This is for Common API Test");
				
System.out.println(obj.toString());
				method.setRequestBody(obj.toString());
				con.executeMethod(method);
				src = method.getResponseBodyAsString();

			// get method

				
				if(token.indexOf(":") != -1) token = token.substring(token.indexOf(":")+1).trim();
				gmethod = new GetMethod("http://192.168.1.197:8900/CommonApis/sourceprofileslist");  // url
				gmethod.setRequestHeader("ova-auth-token",token); // token

				obj = new JSONObject();
				System.out.println(obj.toString());
				con.executeMethod(gmethod);
				src = gmethod.getResponseBodyAsString();
	}
}</pre>
# List of Error Codes
<table>
    <tr>
        <td>Code</td>
        <td>Message</td>
        <td>Description</td>
    </tr>
    <tr>
        <td>200</td>
        <td>OK</td>
        <td>The request is OK</td>
    </tr>
    <tr>
        <td>301</td>
        <td>Moved Permanently</td>
        <td>The requested page has moved to a new url</td>
    </tr>
    <tr>
        <td>400</td>
        <td>Bad Request</td>
        <td>The server did not understand the request</td>
    </tr>
    <tr>
        <td>401</td>
        <td>Unauthorized</td>
        <td>The requested page needs a username and a </td>
    </tr>
    <tr>
        <td>404</td>
        <td>Not Found</td>
        <td>The server cannot find the requested page.</td>
    </tr>
    <tr>
        <td>405</td>
        <td>Method Not Allowed</td>
        <td>The method specified in the request is not allowed.</td>
    </tr>
    <tr>
        <td>415</td>
        <td>Unsupported Media Type</td>
        <td>The server will not accept the request, because the media type is not supported.</td>
    </tr>
    <tr>
        <td>500</td>
        <td>Internal Server Error</td>
        <td>The request was not completed. The server met an unexpected condition.</td>
    </tr>
    <tr>
        <td>501</td>
        <td>Not Implemented</td>
        <td>The request was not completed. The server did not support the functionality required.</td>
    </tr>
    <tr>
        <td>502</td>
        <td>Bad Gateway</td>
        <td>The request was not completed. The server received an invalid response from the upstream server.</td>
    </tr>
    <tr>
        <td>503</td>
        <td>Service Unavailable</td>
        <td>The request was not completed. The server is temporarily overloading or down.</td>
    </tr>
    <tr>
        <td>504</td>
        <td>Gateway Timeout</td>
        <td>The gateway has timed out.</td>
    </tr>
    <tr>
        <td>505</td>
        <td>HTTP Version Not Supported</td>
        <td>The server does not support the "http protocol" version.</td>
    </tr>
</table>

# List of Common APIs
