<h1>Own2Mesh</h1>
<i>Facilitated communication, security and certainty in dealing with complicated rights relationships of distributed applications.</i>
<hr><br>
<img src="https://drive.google.com/uc?export=view&id=1mzfkhE5fXqLGa2lmQNlAu_t9UxbfFKZm" width="140">
<img src="https://drive.google.com/uc?export=view&id=1lyfEl0BTVxmncZEBJFo4C0tmLmju3uv_" width="140">
<img src="https://drive.google.com/uc?export=view&id=1TUXayQA7gJRC185K11CNHoOzhgrfAfyj" width="140">
<img src="https://drive.google.com/uc?export=view&id=1RF-jRIwchbmIppiz-r8Q7jQ4oJniKVvr" width="140">
<br>
<!-- <img src="https://raw.githubusercontent.com/marfrede/O2M_Backend/master/public/imgs/desk.jpg" alt="Developer Desk" width="800px"/> -->
<hr><br>

<h1>Quick Start</h1>
<i> In order to use our API, a free of charge registration is needed in order to get your AppAPiKey! Visit <a href="{{web_url}}" target="_blank">our Backend</a> and create your first application! To do that, follow below instructions if needed.</i>
<li>👩 <a href="{{web_url}}/companies/register">Create an account</a></li>
<li>🌈 Look at your inspiring <a href="{{web_url}}">custom homepage</a></li>
<li>🪐 <a href="{{web_url}}">Create an application</a> with one click 🖱 to start using our Backend!</li>
<li>🔑 Now that you have registered your application you can see your <b>AppApiKey</b> at the bottom of your <a href="{{web_url}}">Application Card</a></li>
<li>🛠 <a href="click">Click</a> the AppApiKey to copy it to your clipboard, safe it and make sure it doesn't fall into the wrong hands!</li>
<li>🚀 You are ready to go! 🎉</li>
<img src="https://raw.githubusercontent.com/marfrede/O2M_Backend/master/public/imgs/guide/guide4.PNG" width="800px"/>
<hr><br>

<h1>Authentification</h1>
<ul>
<li>Our API distinguishes two different types of authentication
<table>
<tr>
<th>App Authentification 🌍</th>
<th>User Authentification 👴</th>
</tr>
<tr>
<td>used for all routes like <b>api/app/*</b></td>
<td>used for all routes like <b>api/*</b></td>
</tr>
<tr>
<td>used to get <b>app specific resources</b><br><i>e.g. all locks of this application</i></td>
<td>used to get <b>user specific resources</b><br><i>e.g. all locks a user owns</i></td>
</tr>
<tr>
<td>Every app has its own <b>AppApiKey</b></td>
<td>Every user has its own <b>UserApiKey</b> also referred to as <b>Token</b></td>
</tr>
<tr>
<td colspan="2">both handed over as <b>Bearer Token</b> in the Header Field Authorization</td>
</tr>
<tr>
<td>Get it at <a href="{{web_url}}">{{web_url}}</a> now by creating an application!</td>
<td>Get it by using <code><a href="#f45487ce-f41f-40b8-993f-132ce62843ec">POST auth</a></code> with the Users ID you got from <code><a href="#81feb18d-8429-493d-bd98-f0be56890565">POST app/users</a></code>!</td>
</tr>
<tr>
<table>
</li>
<li>With the exception of the route <code><a href="#f45487ce-f41f-40b8-993f-132ce62843ec">POST auth</a></code> either the <b>AppApiKey</b> 
 or <b>UserApiKey</b> is required.</b></li>
<li>Thus <code><a href="#f45487ce-f41f-40b8-993f-132ce62843ec">POST auth</a></code> is the only route that works without the Authorization Header Field.</li>
</ul> 
<hr><br>

<h1>Role System</h1>
<p>In our application each user is assigned a role.</p>
<p>There are 3 different roles:</p>
<li><b>Allner</b></li>
<li><b>Manallger</b></li>
<li><b>Consumer</b></li>
These three roles are in a hierarchy as shown above. This means that the <b>Consumer</b> has the least permissions. The <b>Manallger</b> may do <b>everything</b> that the consumer is allowed to do, but has additional permissions. The <b>Allner</b> may again do <b>everything</b> that the Manallger is allowed to do, but again has additional permissions.<br><br>

<table>
<tr>
<th>Allner</th>
<td>The Allner <b>owns</b> locks. He can <b>store</b> locks himself. He can <b>appoint Manallgers</b> for his locks. He can <b>open</b> his locks <b>anytime</b>. He determines <b>which user may open</b> which lock and when.</td>
</tr>
<tr>
<th>Manallger</th>
<td>The Manallger <b>manages</b> locks. He can <b>open</b> the locks he manages <b>anytime</b>. He determines <b>which user may open</b> which lock and when.<br><br> When it is said that a user has a <b>License</b> for a lock, it means that he is the <b>Manager</b> of that lock.</td>
</tr>
<tr>
<th>Consumer</th>
<td>The Consumer only can open locks. To actually be able to do this he is <b>dependent on Allner or Manallger</b>. <br><br> When it is said that a user has an <b>OpenPermission</b> for a lock, it means that he can open the lock under specified conditions (date & time).</td>
</tr>
</table></p>
<hr><br>

<h1>Terms</h1>
<table>
<tr>
<th>Allner</th>
<td>A person who is entitled to <b>own locks</b>, but does not necessarily do so.</td>
</tr>
<tr>
<th>Owner</th>
<td>A person who owns a lock.</td>
</tr>
<tr>
<th>Manallger</th>
<td>A person who is entitled to <b>manage locks</b>, but does not necessarily has a License to a specific Lock.</td>
</tr>
<tr>
<th>Manager</th>
<td>A person who manages a Lock and therefore has a License.</td>
</tr>
<tr>
<th>Consumer</th>
<td>The Standard role of a user. A user, who does not need special rights, automatically slips into the role of the Consumer.</td>
</tr>
</table>

<p>
<b>ℹ Information</b>
<li>If our API mentions a specific role to which this route applies, then this route automatically applies to all roles higher in the hierarchy.</li>
<li>An example: The route <code><a href="#a22a4685-ee67-4d31-8491-12a0904eac8b">GET locks/{{lock_id}}/open</a></code> provides for a consumer as role. The route is used to query all his OpenPermissions for a particular lock. This does not exclude the Manallgers and Allners of our system. An Allner who owns a number of locks can occur as a consumer for other locks that are not his own. Accordingly, an allner would also receive all his OpenPermissions that have been granted to him to open the foreign lock.</li>
<li>So if you want to create a user who can own his own locks as well as manage and open other locks, this user does NOT need all three roles, but only those of the Allner.</li>
<li>It is not possible to assign multiple roles to a user.</li>
<li> It is not possible for a user of a higher role to deny rights of lower roles as he automatically inherits them.</li>
</p>

<table>
<tr>
<th>Lock</th>
<td>The lock plays the central role in our system. Locks can be owned, managed and opened. Who is allowed to do what and when is determined by the person in charge and then strictly adhered to.</td>
</tr>
<tr>
<th>License</th>
<td>If a user wants to grant an OpenPermissions for a lock he does not own, this is still possible. To do so, the user must have a license for this lock. Only Manallgers can have licenses.<br>
A license consists of the ID of the lock (<i>which</i> lock can be managed?) and the ID of the manager (<i>who</i> is allowed to manage?).<br>
In order to obtain a licence for a lock, the owner of the lock must grant it to the Manallger.
</td>
</tr>
<tr>
<th>OpenPermission</th>
<td>If a user wants to open a lock he does not own or manage, he must have a OpenPermissions for this lock. Every User can have OpenPermissions.<br>
An OpenPermission consists of the ID of the lock (<i>which</i> lock can be opened?), the ID of the consumer (<i>who</i> can open the lock?), the ID of the manager (<i>by whom</i> was the OpenPermission granted? <i>this can either be the owner of the lock himself or one of the lock managers</i>), a counter (<i>how often</i> can the lock be opened?) and the <a href="#a22a4685-ee67-4d31-8491-12a0904eac8b">Rrule</a> (<i>when</i> can the lock be opened).<br>
In order to obtain an OpenPermission for a lock, the owner or a manger of the lock must grant it to the asking User.
</td>
</tr>
</table>
<hr><br>
<i>Have fun discovering the endpoints</i> 👓🚴‍♂️🌍