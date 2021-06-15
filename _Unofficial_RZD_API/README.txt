![alt text](https://images.unsplash.com/photo-1551651743-580a790aaab9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1489&q=80 "Russian Railway")


The Unofficial RZD (РЖД) API is a Postman collection for easily interfacing the RZD Railway Website. It lets you easily search the [RZD Website](http://www.rzd.ru/) for fares, trains and schedules.

This project was based on my interest of taking the Transsiberian Railway from Germany to Beijing. When I started doing my initial research I noticed that the prices and availabilities heavily vary depending on the date, train and class. Hence I looked for a way to monitor various trains and dates in advance to find one that fits my needs and budget. This collection came out as a by-product of my bigger goal to monitor a large number of connections with a Python service.

> Update: Feel free to check out my blog post on my website [www.alexbilz.com](https://www.alexbilz.com/post/rzd-api-documentation/) if you want a little bit more context or if are looking for a fully working example in Python.

# How the RZD API works

The RZD API has a request scheme that is fairly easy to grasp. For each task there is an endpoint that is usually defined by a parameter called `layer_id` that takes certain parameters (see the specifics of each endpoint below). If the request was valid, the API will respond with a json containing a RID. The response will look similar to this one:

```
{"result":"RID","RID":11406098162,"timestamp":"26.12.2019 14:14:06.673"}
```

Alongside the json the RID the Server will also yield back a SET-Cookie header that has JSESSIONID Cookie. This cookie has to be added to any future requests. Unlike the RID the Cookie JSESSIONID Cookie doesn't change during every request.

The following Postman test script extracts the data and makes them available to the selected environment:

```
pm.test("Fetch RID", function () {
    var jsonData = pm.response.json();
    pm.environment.set("rid", jsonData.RID);
    pm.environment.set('JSESSIONID', pm.cookies.get('JSESSIONID'))
});
```

Afterwards you should be able to get all the actual response by executing `Fetch Data`.

# Useful Ressources

During my research, I found a couple of good  online resources that I could use as a starting point for my work. Please note that some of them are partly or completely in Russian.

* [RZD Website](http://www.rzd.ru/)
* [Api сайта rzd.ru](https://github.com/visavi/rzd-api)