### Installation
Before you get started with Adapt, make sure you [install Node.js](http://nodejs.org/) and [Git](http://git-scm.com/downloads).

All of the components you'll need can be installed with [npm](https://npmjs.org/) which **comes installed with Node.js**

```bash
$ npm install adapt-cli -g
$ npm install grunt-cli -g
```

### Get the Adapt output framework
#### Overview
The output framework is the generic codebase used to create e-learning content – in other words, it is the generic code that runs as part of the e-learning package in the user’s browser when working through an e-learning module based on Adapt. 

#### Installing
You can get the latest version of the framework from our [GitHub repository](/adaptlearning/adapt_framework) using the Adapt Command Line Interface.

```bash
$ adapt create course
```

This will ask you to confirm the name of the course and the branch to download. A directory with the course name will be created and all the Adapt framework files will be downloaded into it. 

Alternatively you can [download](/adaptlearning/adapt_framework/archive/master.zip) it as a ZIP and perform a [manual installation](/adaptlearning/adapt_framework/wiki/Manual-installation-of-the-Adapt-framework).

The output framework contains all the source files and programs required to produce your course. The output framework uses [Grunt](http://gruntjs.com/) to manage the build process and run all of the grunt tasks from your output framework directory.

#### Building
```bash
$ grunt build
```
The build task compiles and compresses your course and prepares it for viewing and distribution. The output is located in the *build* directory.

#### Viewing the build
To view the build package create a local server:
```bash
$ grunt server
```

To emulate a scorm package offline use this instead:
```bash
$ grunt server-scorm
```
Note: to terminate the server ctrl+c

This will now open a browser and navigate to the following URL:
[http://localhost:9001/](http://localhost:9001/)

*N.B.* If you have run the server-scorm task, navigate to this URL to emulate an LMS environment:
[http://localhost:9001/main.html](http://localhost:9001/main.html)

This allows you to test your SCO without the need for a continual upload / update / reupload cycle. Please note that as this emulation uses an iframe, it is not suitable for device testing. It is intended for testing SCORM functionality only. If you do not require SCORM functionality, please run 

```bash
$ adapt uninstall contrib-spoor
$ grunt build
```

The server will display the default menu of the course in your browser with the view appropriate to the device you're using. Any changes to the course will automatically be built and displayed.

**Next** - [[Creating your first course]]