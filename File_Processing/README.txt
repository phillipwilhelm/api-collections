This collection is for testing file uploads, simulating file downloads (using javascript and visualizer), and simulating file visualization (using visualizer). This collection will set up the necessary html to visualize a file in your browser. Before doing that, you will need to edit the Content Security Policy and allow the proper directives. Refer to the link below for information on Content Security Policy directives.

In particular edit the following:

frame-src data: http: https:;
object-src data: http: https:;

This will allow visualization in the browser.

https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy