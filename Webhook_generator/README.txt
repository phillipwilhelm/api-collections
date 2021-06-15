A simple collection to generate webhooksURL for a monitor of your collection

---

**NOTE**

To run this collection you will need the following environment variables



---


| key          | type   | description                                                                                                                    |
|--------------|--------|--------------------------------------------------------------------------------------------------------------------------------|
| command      | string | `command` is a string that contains the command that initiated the request from slack. Eg: `/cnb_init`                         |
| text         | string | `text` contains the message that was send along side the command. Eg: in `/cnb_guess team` "team" would be the value of `text` |
| response_url | string | `response_url` is the slack webhook where we send the response to each command.                                                |
| user_name    | string | `user_name` is the slack username of the user. We are using it to identify players                                             |