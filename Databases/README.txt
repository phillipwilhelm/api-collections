This collection exists to show you how you can connect to some popular database options through Postman. Typically databases don't offer any form of REST API by default, so you'll need a little bit of extra tooling to get things going - covered below!

It's important to remember that connecting to and querying a database is dependent on this additional tooling - Postman is geared up to be a REST client, not a database client. Recommend looking at SequelPro/Postico for that.

**These setups are typically not something you would run on production, therefore this guide is provided as is and all reasonable care should be taken to work with a safe environment and ensure the right backups are in place.**

Ensure you set your `db_table` environment variable to the table you're looking to work with.

Check out the tooling used in each example to see the full API for how you can query different parts of your database. This collection just includes the basics for each - retrieving all rows from a given table.

In the following examples, we're working with a database called `test_db` and a table called `test_table` with the following data:

| id 	| firstName 	| lastName 	|
|----	|-----------	|----------	|
| 1  	| Joe       	| Bloggs   	|
| 2  	| Ben       	| Smith    	|
| 3  	| Sue       	| Brown    	|
