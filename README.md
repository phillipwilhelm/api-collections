# Github apis in dothttp



clone this repo, open repo in vscode and open a `.http` file (or github codespaces).

configure/update values in [./.dothttp.json](.dothttp.json).


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





               MMM.           .MMM
               MMMMMMMMMMMMMMMMMMM
               MMMMMMMMMMMMMMMMMMM      __________________________________
              MMMMMMMMMMMMMMMMMMMMM    |                                  |
             MMMMMMMMMMMMMMMMMMMMMMM   | github apis with ease checkout   |
            MMMMMMMMMMMMMMMMMMMMMMMM   |_   ______________________________|
            MMMM::- -:::::::- -::MMMM    |/
             MM~:~ 00~:::::~ 00~:~MM
        .. MMMMM::.00:::+:::.00::MMMMM ..
              .MM::::: ._. :::::MM.
                 MMMM;:::::;MMMM
          -MM        MMMMMMM
          ^  M+     MMMMMMMMM
              MMMMMMM MM MM MM
                   MM MM MM MM
                   MM MM MM MM
                .~~MM~MM~MM~MM~~.
             ~~~~MM:~MM~~~MM~:MM~~~~
            ~~~~~~==~==~~~==~==~~~~~~
             ~~~~~~==~==~==~==~~~~~~
                 :~==~==~==~==~~
