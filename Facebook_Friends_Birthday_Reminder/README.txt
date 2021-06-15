Let's admit it. We no longer remember our friends birthdays. We rely on systems like Facebook, Instagram stories or our mutual friends post to remind us of our friend's birthdays. 

These systems can fail to somehow alert you of your friend's special day. Either you didn't visit Facebook today or you missed your mutual friend's post, the regret is heavy and painful.

Introducing **Facebook Friends Birthday Reminder Collection**. Just dump Facebook birthdays data and this collection will start sending you notification one day in advance at your preferred hour.

## Get started
#### 1. Import the collection 
* Click on Run in Postman button to import the collection and the environment.

#### 2. Importing Facebook Birthdays Data
* Login to Facebook and visit https://www.facebook.com/events.
* Click on **Birthdays** link placed on the bottom right hand corner. 
* This will download a file with name `u<id>.ical`.

#### 3. Converting ical to json
* Make sure you have npm installed. 
* We will use **ical2json** for this job. Run `npm install ical2json`.
* Run `ical2json u<id>.ical`. 
* This will save a file called `u<id>.json`.
* Copy the entire contents of the file and set it as `birthdays` env variable inside **Birthday Reminder** environment.

#### 4. Setting up Slack
* Head over to https://api.slack.com/apps.
* Create a new app with `Incoming Webhooks` functionality. 
* Copy that webhook url and set it as `slackUrl` env variable in the **Birthday Reminder** environment.

#### 5. Setting up reminders 
* Create a monitor to check for birthdays and send a slack messahe at your preferred fequency and time.

___

P.S Don't forget to update the birthdays as you keep making new friends on Facebook.

##### Now, never miss a birthday!

![Alt Text](https://media.giphy.com/media/xUOrw4tlQfCTGmD5Kw/giphy.gif)