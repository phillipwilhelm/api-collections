A simple collection to enforce the presence of MFA for human users in an AWS organization.

This is done as follows:
1. List all human users (users with console sign in access)
2. Stringify and save the acquired list of human users to an environment variable.
3. Using `postman.setNextRequest`, iterate over the list of users, maintaining an `index` environment variable to represent the current user being audited.
4. Fetch the MFA device details to determine the current MFA state for the current user. If MFA is disabled, fail a test and add the user's name to a separate list for users that do not have MFA enabled.
5. Compile the non-MFA list users to be sent to Slack as a daily report.

The following environment variables are required by this collection:
| SNo | Variable          | Description                                                                  | Required |
|-----|-------------------|------------------------------------------------------------------------------|----------|
| 1   | id                | The AWS Access Key ID                                                        | Yes      |
| 2   | key               | The AWS Access Key Secret                                                    | Yes      |
| 3   | slack_webhook_url | The Slack webhook URL for sending Slack reports                              | Yes      |
| 4   | slack_channel     | The # prefixed channel name to send Slack reports to                         | Yes      |
| 5   | slack_username    | The username with which to send notifications. Defaults to aws-iam-audit-bot | No       |
| 6   | slack_icon        | The icon used for the Slack message. Defaults to :closed_lock_with_key:      | No       |

Note: While creating the AWS access key and ID, ensure the following:
1. The access key id and secret are not associated with an account that has console login access.
2. The access key id and secret must be associated with a bot user that has the following permissions:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
          "Sid": "GrantUserCumMFAAccess",
            "Effect": "Allow",
            "Action": [
                "iam:ListUsers",
                "iam:ListMFADevices"
            ],
            "Resource": "*"
        }
    ]
}
```

More reading:
1. To enforce MFA for your AWS accounts, see http://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_users-self-manage-mfa-and-creds.html