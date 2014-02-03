### Installation
Before you get started with Adapt, make sure you [install Node.js](http://nodejs.org/) and [Git](http://git-scm.com/downloads).

All of the components you'll need can be installed with [npm](https://npmjs.org/) which **comes installed with Node.js**

```bash
$ npm install adapt-cli -g
$ npm install grunt-cli -g
$ npm install bower -g
```

### Get the Adapt output framework
#### Overview
The output framework is the generic codebase used to create e-learning content – in other words, it is the generic code that runs as part of the e-learning package in the user’s browser when working through an e-learning module based on Adapt. 

#### Installing
You can get the latest version of the framework from our [GitHub repository](https://github.com/adaptlearning/adapt_framework). You should clone the repository using git.

```bash
$ git clone https://github.com/adaptlearning/adapt_framework.git adapt/framework
$ cd adapt/framework
$ npm install
```

Alternatively you can [download](https://github.com/adaptlearning/adapt_framework/archive/master.zip) it as a ZIP and extract it.

The output framework contains all the source files and programs required to produce your course. The output framework uses [Grunt](http://gruntjs.com/) to manage the build process and run all of the grunt tasks from your output framework directory.

#### The Core Bundle
In order to for an Adapt course to run correctly, you will need to install the Core Bundle. This bundle contains a variety of basic components, as well as a vanilla theme used to style and display the course.

*-todo- add menu information once it is contained within the bunde*

To install the core bundle, enter the following command:
```bash
$ adapt install
```

#### Building
```bash
$ grunt build
```
The build task compiles and compresses your course and prepares it for distribution. The output is located in the *build* directory.

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

The server will display the default menu of the course in your device browser with the view appropriate to the device you're using. Any changes to the course will automatically be displayed.

**Next** - [Creating your first course](https://github.com/adaptlearning/adapt_framework/wiki/Creating-your-first-course)