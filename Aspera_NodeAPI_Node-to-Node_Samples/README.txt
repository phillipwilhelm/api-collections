## Postman sample collection for demo Aspera NodeAPI Node-to-Node transfers

all transfers happen with *demo.asperasoft.com*  as the source server and 
*eudemo.asperademo.com* as the target server.  

This sample always transfer 

    source file: "/aspera-test-dir-tiny/200KB.1" 
    destination: "/Upload"
    
but the transfer can be an upload (demo server is sending) or a download (eudemo is receiving) this is to show both possibilities.

For the sample we use the NodeAPI (HTTP user):

    user: "asperaweb"
    password: "demoaspera"

The corresponding system users (linux user) has the same credentials:

    user: "asperaweb"
    password: "demoaspera"

#### There are 5 different sections:

0. test if API is there and accessible
1. browse source and target server
2. simple n2n transfers with "hardcoded" authorization
3. more typical n2n transfer with transfer token based "dynamic" authorization
4. check the status of a transfer

#### more info see
https://developer.ibm.com/aspera/docs/aspera-api-tutorials-use-cases/node-node-transfer-authentication-authorization/

https://developer.asperasoft.com/web/node/ops-transfers