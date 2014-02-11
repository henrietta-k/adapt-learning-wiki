Developing a course takes place in the adapt_framework/src/course folder.  When you want to test or release your creation, there are a few simple commands you should be aware of.

In a Node.js Command Prompt, navigate to the adapt_framework directory.  From here there are several commands you can run:

If your course is intented to track SCORM within a LMS (like Moodle), you should run the following command to insert tracking identifiers:
```
grunt tracking-insert
```
Now, to compile a developer friendly version of your course, run:
```
grunt dev
```

To compile a production ready/minified version of your course, run:
```
grunt build
```

To use launch a stand-alone Node.JS web server and launch your default web browser to preview your course content.
```
grunt server-scorm
```

##Creating the SCORM package
After running the 'grunt dev' or 'grunt build' taks, a /build folder will be created.  Provided that no errors have occured, the contents of this folder can simply be zipped up to create a valid SCORM package.

