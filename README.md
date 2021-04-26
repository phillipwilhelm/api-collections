# Github apis in dothttp

clone this repo, open repo in vscode and open a `.http` file.

configure/update values in (.dothttp.json)[./.dothttp.json]


for authenticated requests you will want to add headers like below

```json
{
    "headers": {
        "Authorization": "Basic <base64_encoded_username_and_token>"
    }
}
```

for information on dothttp visit [here](http://docs.dothttp.dev/)

try dothttp on browser via playground [here](https://ghpage.dothttp.dev/)

It is an unofficial repo, for official api docs look [here](https://docs.github.com/en/rest/) 
