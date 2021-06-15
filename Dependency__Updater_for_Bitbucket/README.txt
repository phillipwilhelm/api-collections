**Dependency Updater for Bitbucket** is the service you can use to keep dependencies of your javascript application hosted on Bitbucket up to date. It checks the latest versions of the dependencies and creates a pull request when an update is available.

It can be set up in a Postman Monitor to perform periodic checks.


#### The postman collection has the following variables - 

| Name              | Description                                   |
|-------------------|-----------------------------------------------|
| user              | Username of the Bitbucket account             |
| appPassword       | Created app password of the Bitbucket account |
| author            | Author of the update dependency commit        |
| owner             | Owner of the repository                       |
| repo              | Repository name                               |