### Installation
Before you get started with Adapt, make sure you [install Node.js](http://nodejs.org/).

All of the components you'll need can be installed with [npm](https://npmjs.org/) which **comes installed with Node.js**

```js
npm install adapt-cli -g
npm install grunt-cli -g
npm install bower -g
```

### Get the Adapt output framework
#### Overview
The output framework is the generic codebase used to create e-learning content – in other words, it is the generic code that runs as part of the e-learning package in the user’s browser when working through an e-learning module based on Adapt. 

#### Installing
You can get the latest version of the framework from our [GitHub repository](https://github.com/adaptlearning/adapt_framework). You should clone the repository using git.

```bash
$ git clone git@github.com:adaptlearning/adapt_framework.git adapt
$ cd adapt
```

Alternatively you can [download](https://github.com/adaptlearning/adapt_framework/archive/master.zip) it as a ZIP and extract it.

The output framework contains all the source files and programs required to produce your course. The output framework uses [Grunt](http://gruntjs.com/) to manage the build process. Run all of the grunt tasks from your output framework directory.

#### Building
```bash
grunt build
```
The build task compiles and compresses your course and prepares it for distribution. The output is located in the *build* directory.

_TODO - How do I view the built output in a browser? How do I create a local server?_


**Next** - [Creating your first course](https://github.com/adaptlearning/adapt_framework/wiki/Creating-your-first-course)