Here is how you can delete the API using the Postman API.
1) Fetch all of the API key Id. \
2) Delete the API using the second request else you can also directly delete the API by running the below curl command in the terminal:

curl --location --request DELETE 'https://api.getpostman.com/apis/{api-id}' --header 'x-api-key: {api-key}'
