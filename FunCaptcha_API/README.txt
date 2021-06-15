----
# Overview

The FunCaptcha API has support for many different obfuscation methods which makes the requests slightly different for every service. For example, some captcha images are AES256 encrypted while other are not. I have attempted to make this documentation cover a variety of obfuscation methods but I can guarantee that there are some cases that I have missed.

----
# Authentication

Requests are typically authenticated with a session token and or a game token. 

## Session Token
You must initially send a request to [/fc/gt2/public_key/](#d1c662c3-a421-46a3-bec9-b078e141ecdb) in order to obtain the session token and other vital information. 

## Game Token
After obtaining the session token, you must send a request to [/fc/gfct/](#ea412171-eca6-474a-ad3e-907f843607d6) to recieve the game token and even more important data like the captcha images and the images rotation increment.

----
# Common Errors

Most requests will return 200 even if there is an error, however, some requests have specific causes for errors.

## /fc/gt2/public_key/
The BDA, or browser fingerprint, that is sent in the initial request to [/fc/gt2/public_key/](#d1c662c3-a421-46a3-bec9-b078e141ecdb) may seem insignificant, however, an incorrect fingerprint will silently return a captcha that will not be solvable. 

## /fc/a/
**ACCESS DENIED** - Access denied is return when the `guess` parameter is incorrectly encrypted 

----
# Rate limit

If there is a rate limit, I have yet to reach it.