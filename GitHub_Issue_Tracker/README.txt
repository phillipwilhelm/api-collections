# This collection helps a user track issues on GitHub that were reported by him/her (or a specific user)

**The collection works as follows**
* Fetch list of all notifiations for the username specified
* Filter the notifications to find the ones reported by the username specified.
* Send out a slack notification with link to the Issues

## Config
Edit the environment to update the following before you start to use this:
* `github_username` : The username for which the issues will be tracked.
* `github_repo` : GitHub repository which will be tracked example: postmanlabs/postman-app-suppor 
* `github_key` : This is the personal access token for GitHub APIs, can be created from here: https://github.com/settings/tokens
* `github_key_username`: Username to use for GitHub APIs. This will be the same username that you created the API key for (`github_username` and `github_key_username` can be same if you are tracking your account and using your account to run GitHub APIs)
* `slack_hook` : Incoming Slack Hook URL : You will need to create a slack app and add an incomin hook to this app : https://api.slack.com/incoming-webhooks - Once the hook is created, copy the URL value for this variable.

## Dependency
The collection relies on a script to be running locally, which is needed to write the data down to disk. As well as to fetch this data by subsequent requests.

**Here is an example PHP script that you may run locally**
_Feel free to implement something similar in the language of your choice_
```
<?php

if(isset($_GET["mine"]) &&  ( $_GET["mine"]=== "true")) {
    
    $FH = fopen("./github_my_issues.csv", "a") or die("Unable to open file 1");
    if($_POST["issue_id"] !== "-1") { 
        fwrite($FH, $_POST["issue_id"]."\r\n") or die("Unable to write file 1");
    }
    fclose($FH) or die ("Unable to close file 1");

} else {

    $FH = fopen("./github_my_issues.csv", "w") or die("Unable to open file 1");
    fwrite($FH, "issue_id\r\n") or die("Unable to write file 1");
    fclose($FH) or die ("Unable to close file 1");

    $FH = fopen("./github_issues.csv","w") or die("Unable to open file 2 for writing!");
    

    $data = json_decode($_POST["notificationData"]) or die("Unable to decode data");

    fwrite($FH, "issue_id\r\n");
    foreach($data as $key => $value) {
        $id = explode("/", $value)[7];
        fwrite($FH, $id."\r\n") or die("Unable to write to file 2!");
    }
    fclose($FH) or die ("Unable to close file 2");

}
```

We use the CSV files created by the above PHP script to perform a "Run".
So for that, the collection needs to be run as follows

```bash
# Fetch notifications and write to CSV
newman run --folder "Fetch GitHub Notification"  "Github Issue Tracker.postman_collection.json" -e "GitHub.postman_environment.json"

# Use the CSV to filter out issues that were crated by the specified username and write to another CSV
newman run --folder "Process GitHub Notifications" "Github Issue Tracker.postman_collection.json" -e "GitHub.postman_environment.json" -d ./github_issues.csv

# Send out slack notifications by reading the second CSV file
newman run --folder "Send Slack Notification" "postman-collection/Github Issue Tracker.postman_collection.json" -d ./github_my_issues.csv -e "GitHub.postman_environment.json" 

```

You may put the above in a bash / batch script and run as a cron job or a a scheduled job on your machine.