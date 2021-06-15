https://community.postman.com/t/how-to-test-if-an-environment-variable-is-defined/1216

We have a `pm.environment.has` API to check if the environment has a particular  key(variable) defined.

This would be the test you're looking for 
```js
pm.test('foo should exist', function () {
    pm.expect(pm.environment.has('foo')).to.equal(true);
});
```

This is also supported as `pm.globals.has`.

Here's a complete API reference of the Postman Sandbox for reference - https://www.getpostman.com/docs/v6/postman/scripts/postman_sandbox_api_reference