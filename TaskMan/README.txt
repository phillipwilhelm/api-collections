#### Features of TaskMan
- [x] Add and assign tasks to any user
- [x] Features priority wise task sorting
- [x] List Completed/Pending/All tasks for any user
- [x] Error handling
- [x] Command Hints
- [x] Supports raw Air DB Queries for tasks
- [x] Highly extensible due to object oriented design

#### Request Lifecycle in TaskMan [Postman Collection]
![Lifecycle](https://raw.githubusercontent.com/pitss-official/TaskMan/main/Screenshot%20(34).png)
- Slack sends the command data as payload to the Dynamic Monitor Invoke webhook
- Request hits the App Request prescript block
- Command Register gets constructed
- Command Classes gets registered
- Dynamic Command based on slack payload gets pulled from the register
- Commander gets constructed
- Commander calls `prepare()` and `next()` methods of the command class
- Command class decides which Postman Request is to be called next and prepares payload for it
- Payload is used by the next request to create an API call and checks for errors and prepare payload for next postman request [Response]
- Final payload crafted and sent back to slack

#### List of commands supported by TaskMan

##### [LISTING & FETCHING]
- [x] list all incomplete tasks assigned to me `/tasks` 
- [x] list all tasks assigned to me `/tasks all`
- [x] show all of my completed tasks `/tasks completed`
- [x] list all incomplete tasks assigned to this user `/tasksfor @user.handle`
- [x] list all tasks assigned to this user `/tasksfor @user.handle all`
- [x] show all of my completed this user `/tasksfor @user.handle completed`
##### [CREATING & ASSIGNING]
- [x] Creating a task `/taskmake taskname startdate enddate user priority? reference?`
##### [MARKING & DELETING]
- [x] mark a task complete with id `/taskmark id notes`
- [x] delete a task `/taskdel id` 
##### [RAW QUERIES]
- [x] Raw filter queries `/tasks unescaped query`
     >Visit 
[Air Table Filter Query](https://support.airtable.com/hc/en-us/articles/203255215-Formula-Field-Reference)
    for more details.
     >
     > Example: `/tasks unescaped AND(IS_AFTER(end,TODAY()),AND(status='completed',associated_users='pawan.kumar'))`
##### [HINTS]
- [x] See all syntax and possible queries `/taskman`

Routing Table
-
| Slack Command | Description                                  | Underlying Command Handler | Routed To [Postman Request] |
|---------------|----------------------------------------------|----------------------------|-----------------------------|
| /tasks        | List tasks according to various type of args | ListMyTasksCommand         | ListTasks                   |
| /taskman      | List hints for all possible commands         | HintCommand                | <NOT ROUTED>                |
| /tasksfor     | List tasks for other users                   | ListOtherUserTasksCommand  | ListTasks                   |'
| /taskmake     | Create and assign task to user               | CreateTaskCommand          | CreateTask                  |
| /taskmark     | Updates the task to completed                | TaskMarkComplete           | MarkComplete                |
| /taskdel      | Delete and a task                            | TaskDelete                 | DeleteTask                  |


Command Extension [creating own command inside TaskMan]
-
In order to extend the application functionality, you can create your own slack commands

For that visit https://api.slack.com and navigate to slash commands
![Slash Commands](https://raw.githubusercontent.com/pitss-official/TaskMan/main/slack.png)

Click on create new command

![Create Slack Command](https://raw.githubusercontent.com/pitss-official/TaskMan/main/create%20command.png)

After creating the slack command lets create the Command Class to handle it 
```ecmascript 6

class MyNewCommand extends Command{
    before(){
        // [optional]
        // this method will be evaluated before prepare() method
        // by commander class
        return  super.before();
    }
    get identifier(){
        // [mandatory]
        // this is slack command identifier and should exactly 
        // match with the slash command as in slack api console
        return "/slackCommandName"
    }
    prepare(args:Array, commandRegister:CommandRegister){
        // [mandatory]
        // this method is responsible for all business logic of the
        // slack command. Here we make payload and set as postman
        // environment variable
        // args are the arguments received from slack
    } 
    next(){
        // [optional method]
        // this method will be called after preparing payload
        // here you can perform Postman Request chaining
        // or can stop further propagation of the request
        // by default the request is not forwarded anywhere
        postman.setNextRequest("MyDestination"); 
    }
    get preResponseMessage(){
        // [optional method]
        // this is the immediate response sent back to slack
        // [caution: this message can be overridden by changing 
        // `pre_response` environment variable inside prepare block]
        return "Going to delete it !!!";
    }
    get name(){
        // [mandatory]
        // this method is used to track the request lifecycle in console
        // it is called during `Commander.run()`
        return "Task delete command"
    }
    get usageHint(){
        // [optional]
        // this method is used by hint command to display
        // how to use this command 
        // if not defined, results in default : this.identifier()
        return "/MyNewCommand";
    }
    get usageDescription(){
        // [optional]
        // this method is used by hint command to display
        // small description as heading in the hint command
        // if not defined, results in default : this.name();
        return null;
    }
    get usageExamples(){
        // [optional]
        // this method is used by hint command to display all the 
        // possible examples that this command can execute
        // if not defined, results in default return through
        // command class (parent class), an empty array which hides example 
        // block from the hints command response
        return [];
    }
}
```
After creating the Command Class you need to register it to autoloader
```ecmascript 6

//inside the Index block
commandRegisterSingleton
    .register(new HintCommand())
    // use method chaining on the registerSingleton to register your 
    // command instances into autoloader
    .register(new MyNewCommand())
```
If your requirement involves further API requests, create a `Request` and `Response` Requests in Postman Collection and utilize the payload made during `prepare()` method call and perform further routing using prescript and test request blocks.

Creating your custom errors
-
All the errors that occur inside App->prescript get handled inside `<Index>` block and details about the error is sent back to slack.

In order to create your own **Error Handling** Mechanism inside TaskMan you can create Error Classes that customizes the way error gets handled and sent back to the user

```ecmascript 6

class MyCustomError extends Error{
    constructor(message) {
        super(message);
        // take the message string here. this message is sent to monitor console and slack
        this.message = message;
    }
    get response(){
        // this method is invoked inside catch block to create payload for slack
        // you can modify the response text or override the text
        return this.message;
    }
    next(){
        // this method is called to chain to the next collection request
        postman.setNextRequest(null);
    }
}
```


Postman Webhook
- 
TaskMan uses Postman webhooks, collections and monitor to function like a **serverless application**


[Note: At the time of writing this document, Postman webhooks are in beta stage]


To create a webhook, we need to create a collection and environment inside Postman, then we can obtain their `id` by sending separate `GET` requests to `https://api.postman.com/collections` and `https://api.postman.com/environments`.

Create a monitor from the above collection with existing environment. You can view details about monitor by visiting your collection->monitors section.

With both `environment_id` and `collection_id`, we can obtain a webhook URL by sending a `POST` request to `https://api.postman.com/webhooks` with the following body and header

Body:
```json5

{
    "webhook":{
        "name": "Name of monitor you want to set",
        "collection": "collection id that you obtain after making api calls",
        "environment": "environment id that this monitor will be linked with"
    }
}
```
x-api-key : `[you need to get the api key from the postman account section]`

The obtained URL in the response can now be used to receive payload from Slack and trigger the monitor on Postman cloud.

upon successful creation on Dynamic invoke able monitor [webhook based] you will get response like
```json5

{
    "webhook": {
        "id": "xxxxxxxxxxx-xxxxx-xxxx-xxxxx-xxxxxxxxxxx",
        "name": "your_monitor_name",
        "collection": "xxxxxxxx-xxxxxx-your-collection-idxxxx-xxxxxxx",
        "environment": "xxxxxxxx-xxxxxx-your-environment-idxxx-xxxxxx",
        "webhookUrl": "https://newman-api.getpostman.com/run/xxxxxxxx/xxxxxxx-xxxxxxx-xxxxxxx-xxxxxxxx",
        "uid": "xxxxxx-xxxxxx-xxxxxx-xxxx-xxxxx-xxxxxxxx"
    }
}
```

use this `webhookUrl` to invoke your collection monitor and follow steps as defined in add command to slack in order to invoke it via slack

**Clone this collection to see how TaskMan works!!!**