Base url: https://instant-transaction.herokuapp.com

an api key is required to use this API. 

request API from API author.



This system allows users to instantly credit their bank accounts or transfer money to other accounts with the value of IDL voucher cards they purchased through USSD.

The system has the functional units: 
1. User Management System
2. The Voucher System
3. The Search
4. The Audit trail


	Bellow is a brief description of each.

1. User Management for IDL

This is a user management system that authenticate and grant privileges to users of idl-voucher app. By the use of proper API_KEY, users are allowed to register. User activation is done through an activation link sent to user's email immediately after registration (ensure to check spam folder, if the link is not in inbox). 

Role (either staff or merchant) is only assigned to users whose acounts are activated. Option exist to re-assign a user a role. In case a user fails to get the activation link, the user can use the "reactivateuser" endpoint to resend an acivation link. 

Finally, "deactivateuser" endpoint is used to deactivate a user.

Note: The API_KEY used in this documentation can change. Always get the API_KEY from the user management admins.



2. Voucher System. This has the following actions:

i. Generate Cards: Here you will need to specify the category it belongs too. type 1 is for card(s) worth 1000, type 2 is for 2000, type 3 is for 5000, type 4 is for 10,000 and type 5 is for 20,000.

ii. Print cards: Here you will need to specify volume and batch number of the card(s) to be printed.

iii. Assign Card

To use this API, accesses printed cards from Voucher pin database.
Only Printed cards should be assigned to Dealer/Merchant.
Only Users with role as Merchant should be assigned cards.

iv. Unassign cards
Here, cards assigned to a dealer/merchant can be revoked. It makes provision to revoke one card by specifying the "serial_no" or for all cards cards by specifying "serial_no":'all'

.Unassigned cards can be reassigned to a diiferent dealer.

v. Card Activation and Deactivation.

This is an API to activate or deactivate card or cards either in bricks(10 cards), bar(10 of 10 or 100), case(bar of 10 or 1000) and pack(case of 10 or 10,000). 

This API must collect two request:
    The serial Number of the card
    The category of the card. The category of the card is represented with 1 for brick, 2 for bar, 3 for case and finally 4 for pack.
    The batch number when a user enters these parameters. first it will check if the serial number exist in the database if TRUE it will execute the next line which is to check the category selected and activate else it will throw invalid serial number NOTE: you can only deactivate an activated card


3. Search: This is a Full-text search engine. It searches through all collections of the database for result.

4. Audit trail:
This service can be called from any unique of the system to log transactions made. Three(3) parameters are required. They are:
 i. userID
ii.  action_type
iii. action_description