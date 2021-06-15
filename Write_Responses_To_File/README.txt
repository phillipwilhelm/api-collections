This collection makes it easy for users who want to write the response of each request to a file.
This can be extended to write anything for eg. meta information or value of variables being used.


This project is using a powerful feature built in postman called as `pm.sendRequest`, the docs for which can be found here: https://www.getpostman.com/docs/v6/postman/scripts/postman_sandbox_api_reference#pmsendrequest


## Requirements
To work with this script, a local server is required.
You can choose to write your own local server or edit the one provided below as per your needs.

## Steps To Use
1. Put all the requests you want to write the responses for, under this collection.
 
2. Clone the following repository to your machine - https://github.com/sivcan/ResponseToFile-Postman or use the following command - `git clone https://github.com/sivcan/ResponseToFile-Postman`

3. Navigate into the directory and install the dependencies. Use the following command: `npm i` 

4. Run the local server. Use the following command: `node script.js`

5. Now, the responses for every request which is a part of this collection will be written to the `Responses` folder inside the project repo.
You can modify the local server's code to change the file location.

5. Run your requests through builder / run through collection runner and store your data locally. 


You can modify the script and the local server to support more data formats / data that you want to write to the file.

## Additionally
Instead of moving each request under this collection, you can copy the script from the `Tests` tab of this collection to the `Tests` tab of any request or even a specific folder.

**Note:** To access the `Tests` script of this collection:
1. You need to `Right Click` the `Write Responses To File` collection in the sidebar.
2. Click on `Edit`
3. Go to `Tests` tab.

Then you can send that particular request / requests under a folder for which the data needs to be written.

## File Extensions
You can also modify the **extension** of the file.

**Example:**
Incase you want to write CSV data to a file, all you need to do is change the `fileExtension` property in the `Tests` script to `csv`.

## File Support
Modify the `opts` variable as per your need under the `Tests` tab of the collection, the following features are supported:

1. If you want all the data to be written to a single file then you can modify the value of `mode` to `appendFile` instead of `writeFile` (More functions here: [Node FS](https://nodejs.org/api/fs.html#fs_fs_writefile_file_data_options_callback))
2. If you want each response to be stored in a different file, then you can provide a uniqueIdentifier such as `Date.now()` or some environment variable as a counter, and it'll be used generate unique file names. You can also make the value of `uniqueIdentifier` as `true` and the server will internally append a unique number to every file name.
