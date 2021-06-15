## Description

The collection make use of REST API exposed by AWS IAM to fetch data related to IAM entities and their access to AWS resources.


The collection processes fetched data using “Pre-request & Post-requests Tests” to detect nonalignment with the AWS IAM audit checklist. 


The audit result is pushed to Slack for further actions for DevOps Team.

---
## Environment Variables
| Environment Key   | Value |
| - | - |
| aws_access_key_id | Read: https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys |
| aws_secret_access_key | Read: https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys |
| slack_url             | Read: https://api.slack.com/incoming-webhooks   |
---

**IAM Audit Checklist**
```
1. Check if root user access keys are disabled.

2. Check if the strong password policy is set for an AWS account. 	
	Minimum password length (10)
	Require at least one lowercase letter
	Require at least one number
	Require at least one non-alphanumeric character
	Allow users to change their own password
	Enable password expiration (365 days)
	Prevent password reuse (24)

3. Identify IAM users(humans) whose active access keys are not being rotated for every 45 days.

4. Identify if IAM users(bots) whose active access keys are not being rotated for every 180 days.

5. Identify IAM users(humans) who are inactive for more than 180 days.

6. Identify IAM users(bots) who are inactive for more than 180 days.

7. Check if the MFA is enabled for IAM users(humans).

8. Identify all the permissive policies attached to the roles.
	Permissive policies : where the value of “Principle” or "Action" is “ * ” (wildcard character).	

9. Identify unused and not recently used (not last accessed in 180 days) permissions provisioned via policies attached with IAM entity (user, group, role, or policy) using service Last Accessed Data.
```