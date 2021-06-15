The Statping API allows you to programmatically access data on your Statping server.

The easiest way to get started with the API is by running your own Docker or local instance of the Statping server.

<img width="100%" src="https://img.cjx.io/statuptokenbalance.gif">

# Authentication

An API Key is required to be sent as part of every request to the Statping API, by using the `Authorization` and the API Secret Key as a header.

> If you do not have an API Secret Key, you can find it on the Settings page.

You can Authenticate by implementing the following...
- Using the `Authorization` header with API Secret Key
- Setting `GO_ENV` to `test` to bypass all authentication
- Adding `?api=<keyhere>` URL Query along with the API Secret Key
- Adding `?api=<userkey>` URL Query along with the API Key for a user
- Being logged into Statping as an admin (using JWT sessions/cookies)

> Authentication will create a cookie named `statping_auth`.

# Environment Variables
Statping includes many environment variables that can give you more control over your instance. Please view the [Environment Variables Wiki](https://github.com/statping/statping/wiki/Environment-Variables) page to view a complete list. Below are a couple important ones...
- `STATPING_DIR` - Statping's working directory. By default, this will be set to the current working directory. This path will contain the `config.yml` file, `logs`, and `assets` folder. 
- `SASS` - Absolute path to the `sass` executable. By default it will attempt to find `sass` in your `$PATH`. 

# Demo
You can checkout the Statping Demo instance at [https://demo.statping.com](https://demo.statping.com). All features are available for you to experiment with. The API Secret Key is `demoapisecret123`. Since this instance is public, it will be reset with sample data **every 90 minutes**.
