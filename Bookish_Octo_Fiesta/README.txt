## Bookish Octo Fiesta gets your 8 books which you may enjoy based on the reviews by the users you follow on Goodreads.


These are the following environment variables which needs to be set:

1. `key`: Goodreads developer key
2. `secret`: Goodreads developer secret
3. `oauthtoken`: OAuth token generated using docker image
4. `oauthsecret`: OAuth secret generated using docker image

### How to generate Goodreads developer key and developer secret?

Sign in to your Goodreads account and visit https://www.goodreads.com/api/keys to generate your keys.

### How to generate oauthtoken and oauthsecret

Run docker container using command `docker run -it aliasgarlabs/bookish-octo-fiesta`. Click on the url printed on the console and authorize Goodreads access. Upon returning back to the console, retreive the oauthtoken and oauthsecret from the screen output and set them as environment variable.


#goodreads #books #api #social #recommendations #read #collection #follow