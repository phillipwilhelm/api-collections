This writes the response of a request to a GitHub file. If the file does not exist it will create it, taking the name of the collection and turning it into the file name.

This collection is meant to be used as a seed for writing any Postman API response to a public or private GitHub repository for easy saving of data to a location that can be integrated into other applications or pipelines.

Requires an environment with three variables:

- github_token - A valid GitHub token, you can issue at https://github.com/settings/tokens.
- github_user - The GitHub user or organizatiobn you wish to be writing data to.
- github_repo - The public or private GitHub repository you wish to be writing data to.

If you have any questions you can tweet at @apievangelist or email info@apievangelist.com.