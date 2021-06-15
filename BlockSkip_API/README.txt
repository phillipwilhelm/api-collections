# Introduction
 The BlockSkip API lets exchanges and wallets integrate any cryptocurrency and token. Covering a full operational service, enable the exchange to create new wallets, check balance and send transactions.

# Overview
For security reasons we do not store private keys, keep them safe with you.

# Authentication
On the free environment you need to send the username and password on every request, so that BlockSkip can check who is calling the API. To get a new one, send an email to support@blockskip.com. 
Important: On the free environment the private key generated is not encrypted, so do not use in your production enviroment, even by https.

On the production enviroment you need to send the key, signature and nonce at every request. All private keys is encrypted.

# Error Codes
400 - Cryptocurrency not supported (like: BTHXO)
401 - Unauthorized

# Rate limit
At free enviroment there is a limit of one request by four seconds.

At production enviroment is hundred requests by second.