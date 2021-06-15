This collection reports the Bitbucket pipelines/Builtkite build status of the latest commit on `develop` branch to Slack.

# Adding a new service

1. Duplicate any one of the `GET` requests that is named after one of our services. For Bitbucket Pipelines, duplicate the request for `Identity Service`/`Sync`. For Buildkite builds, duplicate one of the `Postman Chrome`/`Postman Native` requests.

2. Rename the request to the service that needs to be monitored. For instance, `Domain Service`, `Cloud API`. This name is intended to be human friendly, and should not be the repository name.

3. Under request `Authorization`, ensure that `Basic Auth` is selected from the dropdown menu, with username and password set to `{{username}}` and `{{token}}` respectively. This step should **NOT** be done for Buildkite based builds.

4. Update the repository name in the request url with the appropriate repository name corresponding to your service. For instance, `postman-domainverification-service` for `Domain Service`, and `postman-cloud-api` for `Cloud API`.

5. In the test script of the newly created `GET` build statues request, update the `owners` field on line `23`/`27` to indicate recipients for individual build failure notifications. For Buildkite based builds, ensure that the appropriate `:pipeline` (in the url) and `branch` query param are set correctly, as per the service specifications. Usually, the branch would be `develop`.

6. Re-order the request (if necessary) so that it is placed before the two Slack `POST` requests at the end. Please ensure that alphabetical order among service build status `GET` requests is maintained. The two Slack `POST` requests must always be at the end, such that the individual failure notifications request is at the end.

7. Done.