### Symptom
Upon closing a SCORM course, the LMS doesn't do [something expected] when using a modern browser.

### SCORM overview
The LMS makes a series of standardised, named functions, an API called SCORM, available in JavaScript with which the content JavaScript can interact. The content does not directly communicate with the LMS except through this SCORM API. The back end of the SCORM API, implemented by the LMS, communicates with the LMS on the course's behalf using http requests.

### Problem summary
When the course is closed, the course calls the LMS's SCORM function `LMSFinish`. In this case, the `LMSFinish` function uses a synchronous, or blocking, http request. Modern browsers prevent blocking https requests in order that whilst a request is being performed, the browser window does not hang. Instead, asynchronous or non-blocking http requests are performed so that the browser window stays performant whilst in use.

### Problem use-case
##### Old method
1. [the user clicks the window close button]
2. Window triggers beforeunload event  
   a) LMSFinish starts a blocking request, causing the browser to hang  
   b) LMSFinish finishes a blocking request
3. Window triggers unload event
4. Browser closes
##### New problem
1. [the user clicks the window close button]
2. Window triggers beforeunload event  
   a) LMSFinish starts a non-blocking request (which never finishes)
3. Window triggers unload event
4. Browser closes

### Bad solution
> _Call LMSFinish and wait for it to complete before closing the window_

We could change the way Adapt works to do an asynchronous (non-blocking) http request first, before any call to `window.close`, but `window.close` is only one way of closing the window. We aren't able trap or prevent or stop or delay other methods of closing a window in order to allow a non-blocking call to `LMSFinish` first.

For example, when a user clicks the window's close button, the JavaScript function `window.close` is never called, but the window triggers its unload events - which can't be stopped - Adapt calls `LMSFinish` from a window unload event handler, and then the browser then closes. `LMSFinish` in modern browsers (remember that `LMSFinish` is implemented by the LMS) is now not allowed to make a blocking http request, so if it does, the browser closes before the course's finishing http request is complete.

### Semi solution
You could add an additional close button to your course, which calls `LMSFinish` when clicked, (see [adapt-close](https://github.com/cgkineo/adapt-close)). This won't stop users clicking the window close button and losing their stuff as this isn't an LMS fix for the `LMSFinish` function but it may buy you time until you can fix your LMS.

### Good solution
Fix the LMS.

### References
[beforeunload](https://developer.mozilla.org/en-US/docs/Web/API/WindowEventHandlers/onbeforeunload), [unload](https://developer.mozilla.org/en-US/docs/Web/API/WindowEventHandlers/onunload), [sendBeacon](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon), [fun reading](https://community.trivantis.com/knowledge-base/chrome-80-will-disallow-synch-xhr-page-dismissal/), [more fun reading](https://support.scorm.com/hc/en-us/articles/360035814314-Blocked-SCORM-Exit-Postbacks-with-Google-Chrome-80-and-Above), [and more](https://community.articulate.com/discussions/articulate-storyline/chrome-78-release-on-22-october)
