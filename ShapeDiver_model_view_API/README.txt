Using the ShapeDiver model view API allows to access ShapeDiver models without using the ShapeDiver Viewer. 

This collection documents how to use the ShapeDiver model view API for 

  * requesting and downloading **exports**, and
  * requesting **computations** of the geometric and data outputs
  
provided by ShapeDiver models. Refer to the [documentation of the ShapeDiver Plugin](https://support.shapediver.com/hc/en-us/sections/360003422672-Category-Outputs) to learn how to define exports and outputs.

A **typical workflow for exporting data** using the ShapeDiver model view API consists of these steps: 

  * _Session init request_: Open a session for a ShapeDiver model and retrieve information about it (which parameters and exports exist)
  * _Export request_: Send an export request for the desired export and parameter values
  * _Export download_: Download the result of the export

This workflow may be shortened by combining the _session init request_ and the _export request_ into a single _session init and export request_ as described below.

A **typical workflow for requesting computations** of the geometric and data outputs consists of these steps: 

  * _Session init request_: Open a session for a ShapeDiver model and retrieve information about it (which parameters and outputs exist)
  * _Customization request_: Send a customization request for the desired parameter values
  * _Export download_: Download the result of the export

Import this collection to your Postman account and give it a try. Review the JSON replies and how the test scripts are used to extract data from them.