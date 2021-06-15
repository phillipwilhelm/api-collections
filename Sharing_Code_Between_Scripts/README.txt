This collection is an example of how to share code between scripts.

* Code is stored in an environment variable and can be re-used among different requests and in different collections.
* Look at the Pre-request script on the Collection for an in-depth view on how to set this up.
* Prefer to use `new Function()` over `eval`.  The `Function` constructor executes in the global scope only and prevents polluting the Postman Sandbox with potential security issues.  See more here: [Function() constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/Function).

Look at the Test scripts for both Request 1 and Request 2.  Notice how the code is reused between scripts.  Because this script is stored in an environment variable, it can potentially be used across collections, as well.

Test example:

```js
const validate = new Function(pm.variables.get('validateResponseBody'));

pm.test('verify query params', () => {
    validate(pm);
});
```

To see the test fail, try changing the query parameter `foo` to equal something other than `bar`.