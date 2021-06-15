# Overview
The aim of this collection is to demonstrate how a request from a collection can be reused/referenced in a different collection.

This idea can also be extended to create a repository of scripts and reuse them across different collections.

The only disclaimer here is that you will have to make an extra API call to fetch that request/script.

# Usage
1. Add the script defined in the implementations section as an environment variable against the key `executeReferencedRequest`.
2. Add your [API Key](https://go.pstmn.io/docs-pro-api-intro) as part of the script.
3. Add the following script as part of pre-request or test script, according to your use-case.

``` 
eval(pm.variables.get("executeReferencedRequest"));

executeReferencedRequest({
    collectionUUID: "<COLLECTION_UUID>",
    requestName: "<REQUEST_NAME>"
}, () => {

    eval(pm.variables.get("referencedPreRequestScript"));
    pm.request.update(pm.variables.get("referencedRequest"));
    eval(pm.variables.get("referencedTestScript"));

});
```
Here `<COLLECTION_UUID>` is the UUID of the collection from which you want to reference the request and `<REQUEST_NAME>` is the name of the request that you want to reuse/reference.


`executeReferencedRequest` here will set three local variables which are:
- `referencedPreRequestScript` - Contains the pre-request script of the referenced request.
- `referencedTestScript` - Contains the test script of the referenced request.
- `referencedRequest` - Contains the actual referenced request. 

# Script Implementation
Please refer to this [Gist](https://gist.github.com/prashantagarwal/f278b3ca78b3927cde06f68674b82cae) on Github