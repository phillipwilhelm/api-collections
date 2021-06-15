# Introduction
What does your API do?
1. Download targz file from the internet 
2. Decompress downloaded targz file using decompressed-targz module

# Overview
Things that the developers should know about:
1. node js
2. promise
3. express js
4. extract file using decompress module

# Authentication
What is the preferred way of using the API?
Download link from secured site https

# Error Codes
What errors and status codes can a user expect?
Error 1: wrong url format, 
status: cant proceed to download

Error 2: decompression failure
status: false,
message: "fail to download & decompress,
code: 1

# Rate limit
Is there a limit to the number of requests an user can send?
NO