![test](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/postman.jpg)

# Description

This collection helps in moving other collection under a single collection

Here we get full target collections using postman API

**THIS WONT AFFECT THE ACTUAL COLLECTION**
here we create a new collection json so no negative effects

# Usage instruction

**Authorize postman API**

Goto: Postman account settings and create an API Key.

replace the apikey value with your key

**Replace pre-request information**

Goto **"GEnerate new colelction"** request inside the  **Run in collection runner** folder and update the API key, collection UUID list.

**Now execute the Run in collection runner folder**

Run the **Run in collection runner** folder in collection runner

This creates a new collection and collectionvariable with the required json value

**Execute Download new collection**
This implementation creates a new collection in the current workspace **automatically**

IF you want **json** Send the Download new collection json reqeust , and goto response > body >visualize

**Goto visualise**

Goto visualize and click download as json , you have the new json :)

**IMPORTANT**

![test](https://cdn.searchenginejournal.com/wp-content/uploads/2017/05/shutterstock_389230123-760x400.jpg)


Variables are not supported in folder level so , collection variables are aggregated from each collection and added as collection variable for the new collection ,so duplicate variables might be present please review.