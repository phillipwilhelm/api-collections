<h1>Overview:</h1>
STOP waiting for "Discover Weekly" playlist to show up on Monday mornings. Use this collection to generate On-Demand recommendations that you can control. This collections recommends you on-demand new songs and generates a playlist directly from Slack based on choice of your Spotify library. 

<h1>Authentication:</h1>
This collection needs 3 tier Authentication.<br/>
<h2>1) App Level -</h2> https://developer.spotify.com/documentation/general/guides/app-settings/#register-your-app<br/>
<h2>2) User Level -</h2> https://developer.spotify.com/documentation/general/guides/authorization-guide/#client-credentials-flow<br/>
<h2>3) Scope Level -</h2> https://developer.spotify.com/documentation/general/guides/authorization-guide/#scopes<br/>

<h1>Workflow:</h1><br/>
1) User can generate "Discover Weekly" style playlist with just a single Slack command. This command has 3 params which are seperated by commas.<br/><br/>
	a) First is your choice of Seed: This is where you can control your choice of seed.<br/>
		Example: You can suggest - I want songs recommended base of my "Top" songs or "Liked" songs or perticular "Playlist".<br/><br/>
	b) Second is name of your new playlist where recommended songs will be stored.<br/><br/>
	c) Recommendation type: Here you can control what is the method by which recommendations are generated.<br/>
	Example: There are two types of recommendation - Exact or Range.<br/>
<h5>Example: -</h5> First param should be - choice of seed,Second - Playlist Name,Third - Recommendation type.<br/>
		 - Command will look like this: Top,My New Playlist,Exact<br/>

1) Enter seed of your choice, new playlist name and recomendation type in slack command.<br/>
2) Based on your choices/inputs this collection will decide next steps-
- Just for purpose of understanding I will take the slack command as: Top,My Cool Playlist,Exact.<br/>
- Here, "Top" means - your most listened songs over last month will be selected as seed. "My Cool Playlist" is - name of your newly created playlist. "Exact" means - this collection will recommend you songs that are exactly similar to  the songs of your seed choice (In this case your "Top" songs).<br/> <br/>

3) GET all of your TOP song ID's<br/>
4) GET Raw audio property from each song<br/>
5) GET recommendations based on each songs associated Raw audio property<br/>
6) POST Create a Playlist<br/>
7) POST earlier recommended songs to newly created playlist<br/>
8) GET Playlist URL<br/>
9) POST Newly created playlist will be posted to Slack channel.<br/>
10) Enjoy!<br/>