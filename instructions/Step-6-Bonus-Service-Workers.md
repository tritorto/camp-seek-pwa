## Table of contents

1. [Introduction](README.md)
1. [Setup](Step-1-Setup.md)
1. [Converting to PWA](Step-2-Convert-to-PWA.md)
1. [Architecture](Step-3-Architecture.md)
1. [Responsify](Step-4-Responsify.md)
1. [Security and QA](Step-5-Security-and-QA.md)
1. Service Workers (bonus)
1. [Conclusion](Step-7-Conclusion.md)

# Service Workers (bonus)

Open serviceworker.js and take a moment to browse over the code.

There are 3 methods.

```
self.addEventListener('install', function(e) {  
```

Install is an event that happens when this worker is successfully registered - when the application first loads.


```
self.addEventListener("activate", function (event) {  
```

Activate is an event that happens occurs the first time the worker becomes active - i.e.
when the page is refreshed (hard)


```
self.addEventListener("fetch", function (event) { 
```

The Fetch Event happens when a request is made (every time).
This particular fetch handles delayed caching of other assets based on the response types.

The different response types (listed below) have to be handled differently if you want to cache them.

Response types:
* Basic: hosted on our domain
* CORS: external domain that supports CORS (i.e. full access to the response)
* Opaque: response from another source that doesn't support CORS

## Test
Using Chrome on your computer, open the URL to your weather application (i.e. the https Pancake URL).
Now open up the Chrome developer tools. If you are on Windows, you can press F12 to launch, or on a Mac, Cmd+alt+I will load this.

Now go to the Applications tab and click on ServiceWorkers. You should see your service worker listed there.

If you look in the console, you should see some debug logging showing that the service worker has cached the app shell and is retrieving from the cache.

If you go back to your Applications directory and then click on Cache - you will see the static assets defined in the serviceworker.js file.

### Bonus - Advanced Debugging

If you are familiar with JavaScript debugging, there are some interesting insights on what is going on behind the scenes in the service worker.

If you have time, look at the other tabs within the developer tools - for example, the Sources tab and open up the serviceworker.js file - see if you can put a breakpoint within the fetch method and inspect the objects being used.
