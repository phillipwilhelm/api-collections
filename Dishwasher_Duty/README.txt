## What this Collection Does
Accesses an Airtable to assign "dishwasher duty" for the day. The Airtable contains individuals on the dishwasher rotation, with the number of times they've had dishwasher duty, and their internal slack handle. This collection takes the least-worked person and assigns him/her dishes for the day, then posts the assignment to the office channel in Slack. 

In production, this collection has a monitor running daily Monday-Friday at 8 a.m., thus assigning someone to "dishwasher duty" every working day.

This collection uses an environment to store the API key and the URL to access the Airtable base, both available from Airtable's documentation. It also holds the URL for the Slack webhook, to allow the collection to post to Slack the person assigned to manage the dishwasher each day.