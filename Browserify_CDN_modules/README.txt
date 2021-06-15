This collection demonstrates a pre-request script for Postman collections, folders, or requests that imports packages from npm after bundling them through [Browserify-CDN](https://wzrd.in/).

## Usage

In global, collection, or environment variables, define a variable named `dependencies`
that lists packages to import in the form `<package-name>@<version>`.  To include
multiple packages, separate the package specs with commas
(e.g., `async@latest,debug@4.1.1`).

Then, in pre-request or test scripts, initialize dependency resolution support with
the following code:

```js
new Function(pm.variables.get('init'))(pm);
```

Optionally, include specific packages to require.  This can be helpful if you've
resolved a large number of dependencies but only need specific dependencies for
the current script.

```js
new Function(pm.variables.get('init'))(pm, ['uniq']);
```

> Avoid using `eval()`, when possible, as it can pollute the Postman sandbox scope and 
> potentially alter Postman built-ins.  The `Function` constructor prevents this.
> While `eval()` is supported for the `init` and `clean` scripts, it is not encouraged.

> If using `eval` with the init script, you may enable filtered dependeny resolution
> by declaring a variable named `dependencyFilter` with the specific dependencies listed
> in an array value.  Example: `const dependencyFilter = ['uniq']`.

In practice, it may make sense to include a request in the collection that will clean up
stored dependency variables.  You can do that by executing the following:

```js
new Function(pm.variables.get('clean'))(pm);
```

## Advanced

By default, https://wzrd.in is used as the Browserify CDN.  This project is open source
and can be run independently on infrastructure you control.  You can find the
source on GitHub: https://github.com/browserify/wzrd.in.  To override the Browserify CDN
URL, add a variable (global, collection, or environment) named `browserify-cdn` with the 
custom Browserify CDN service URL (e.g., `http://localhost:8080`).

## Explore this Example

View the pre-request script for the collection.  To use in your own collections, copy and paste 
this script.  You'll also see a `dependencies` variable with a list of dependencies.

After running one of the usage requests, check the variables on the collection again.  You'll
see individual variables for each of the required modules.  The pre-request script will manage these variables.  Feel free to run a `clean` script, as demonstrated in the `Clean Dependencies` request to remove these variables.