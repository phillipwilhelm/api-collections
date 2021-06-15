https://community.postman.com/t/change-request-body-raw-json-dynamicalls/2043

1. Build the body in the form of a JSON object. This happens inside the pre-request script.
```js
var body = {
  id: 'asdas',
  pwd: 'asdas',
  auth: 'ashd'
};
```
2. Stringify the body, using [JSON.stringify](https://developer.mozilla.org/enUS/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify). This converts objects to strings.
```js
var body_str = JSON.stringify(body); // body was defined in the previous step.
```
3. Save the stringified body as an environment variable using `pm.environment.set`;
```js
pm.environment.set('request_body', body_str); // this sets an environment variable with the stringified body
```

4. In the request body editor, specify the `raw` request body as the variable created in step 3.
```
{{request_body}}
```

Note that the snippet from step 4 will have to be placed in the body editor.