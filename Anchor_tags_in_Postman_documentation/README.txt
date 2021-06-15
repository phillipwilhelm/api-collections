## About

This page provides examples of anchor tag usage in Postman documentation!

## Creating Section Headers


## Linking to folders and requests
On any Postman documentation page, each folder and request (as well as the  is assigned a unique anchor tag ID. You can find this by clicking on the request or folder in the left nav bar, and looking at the end of the resulting URL.

Here is an example for the **GET Requests** folder on this page:

https://documenter.getpostman.com/view/5293839/Rztms92o# `c892f021-30c4-4595-9e9d-c877b4423352`

The `id` shown above can be used to link elsewhere in your docs page, using the following Markdown syntax:

`[Link Text](#abcdef01-2345-6789-abcd-ef0123456789)`

The id can't be customized, but it does persist unless the underlying folder or request is deleted.

*Rendered example:*

Sections linked using anchor tags:

* [GET Requests](#c892f021-30c4-4595-9e9d-c877b4423352)
* [POST requests](#ce9344c2-a9ec-4f2f-9203-c41f40e55f8d)