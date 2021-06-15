### Follow along on the livestreams
- [Part 1: Unboxing Philips Hue lights and messing around with their API](https://www.youtube.com/watch?v=Nu0oMwld5Pk&list=PLM-7VG-sgbtClLYusN3pr6UT4SiuqmNEM&index=25)
- [Part 2: Make your own Bat-Signal](https://www.youtube.com/watch?v=BnSM0iurzM4&list=PLM-7VG-sgbtClLYusN3pr6UT4SiuqmNEM&index=14)
- [Part 3: Change a light based on the mood of your tweets](https://www.youtube.com/watch?v=CMyX7RZ21BY&list=PLM-7VG-sgbtClLYusN3pr6UT4SiuqmNEM&index=5)

# Get Started
- Select the folder `Working in Production`
- Find the `POST` request `turn on / off - PROD`
- Update the payload to `{"on": true}`
- Hit **Send**

# More info
Joyce is passing requests through to a Philips Hue lightbulb in her kitchen. The responses you receive from these endpoints are from her proxy server (not the Philips Hue device). If you want to set up something like this in your own home, check out this blog post: [Enable public access to connected devices in your local network](https://medium.com/@joycelin.codes/enable-public-access-to-connected-devices-in-your-local-network-c15338da5a3)

Turn on the lights in Joyce's kitchen by sending requests in the folder **Working in Production**. 

    https://light.meowsergirl.com

Feel free to update the lights during future livestreams in a totally non-distracting way.

Follow [GetPostman on Twitch](https://www.twitch.tv/getpostman) so you never miss an episode! In a previous livestream, we worked locally to `GET` the current weather and update the lights according to the weather forecast. 
- [Code sample on Postman](https://explore.postman.com/templates/9097/hue-for-twitch) for working locally
- [Recording of the livestream](https://youtu.be/Nu0oMwld5Pk)