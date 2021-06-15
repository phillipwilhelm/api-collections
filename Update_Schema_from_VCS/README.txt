# Who this collection is for?

* Someone who wants to automate schema syncing between their Gitlab and Postman instances

# What does this collection do?

* It enables us to update our schema programmatically using the Postman API anytime the YAML Schema is updated on the Gitlab repository

# Setup

* Take a look at: [Collection Variables](https://learning.postman.com/docs/sending-requests/variables/#defining-collection-variables) on how we can update the collection variables
* Take a look at the [Postman API documentation for API](https://documenter.getpostman.com/view/631643/JsLs/#ab083bce-916e-4c19-a280-96c273dea4e4) to learn about the operations currently available using the Postman API. 
* Clone or download the repository from: https://gitlab.com/aahmed.asm/updatemyschemaonpostman.git
* Install NPM and NodeJS
* Update the index.js file appropriately with the directory where the Schema file resides
* Update the config.yml(placeholder) files with the appropriate information
* Move all the relevant files onto your Gitlab instance
* Navigate to the directory and Execute the command 'make'