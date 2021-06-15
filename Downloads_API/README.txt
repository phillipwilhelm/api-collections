The Downloads API allows you to access and download available Tenable products installation files and updates. You can use the API endpoints to list product pages, list downloads available for a specific product, and to download a file. The endpoints can also be used to determine and download the latest version of a file to facilitate the automation of an installation.

**Note:** Tenable Downloads API uses a different server URL than Tenable.io API: `https://www.tenable.com/downloads/api/v2/pages`.

### Authentication

The Downloads API uses Bearer token authentication and requires a valid token in the Authorization header:
```
Authorization: Bearer AbCdEf123456
```

To access or reset your authentication token, navigate to the [Authentication Token](https://www.tenable.com/downloads/api_docs) page.