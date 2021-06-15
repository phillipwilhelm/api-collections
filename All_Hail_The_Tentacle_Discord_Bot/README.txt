Example template on how to make a Discord bot using Postman and Postman Monitors. 

Using a Discord bot to post to a channel through a generated webhook. 

The first thing is to make a bot in the Discord Developer's section. 
https://discordapp.com/developers/applications

Then to add your bot to a server and give it the proper permissions using this link in a web browser. Be sure to update the client_id and the permissions -- which can be done in the bot section of your application to generate the permissions number. 

`https://discordapp.com/api/oauth2/authorize?client_id={{client_id}}&scope=bot&permissions=536942592`
Discsord has a limit of 10 webhooks you can generate so try to use the same webhook generated from a previous request.