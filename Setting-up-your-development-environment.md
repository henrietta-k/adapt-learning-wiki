### Installation
Installing Adapt requires the use of the command line. If your skills are a little rusty, the wiki article [*Just Enough Command Line for Installing*](https://github.com/adaptlearning/adapt_authoring/wiki/Just-Enough-Command-Line-for-Installing) might be all the assistance you need. If you've never used the command line before, please take advantage of tutorials on the web. Adapt does not require you to be an expert with the command line, just familiar with basic terminology and techniques.  

Before you get started with Adapt, you will need to install [Node.js](http://nodejs.org/) and [Git](http://git-scm.com/downloads) if you haven't already done so.

Windows users may prefer [Git for Windows](https://msysgit.github.io/) or [Github for Windows](http://windows.github.com/). Note: if you install Git for Windows, you will need to reboot after installation even though it doesn't prompt you to do this.

OS X 10.9 (Mavericks) users - you should be able to install git simply by trying to run the command 'git' in the Terminal. It should recognise what you are trying to do and prompt you to install the XCode Command Line Tools, which include Git.

Once you've got both Git and Node.js installed, the other components you'll need can be installed with the Node Package Manager - AKA [npm](https://npmjs.org/) - which **comes installed with Node.js**

To install the components, run the following two commands - which can be done via Terminal on OS X or on Windows via whatever command line utility was installed when you installed Git e.g. Git Bash or PoshGit.

OS X users - you will need to either prefix the commands with 'sudo' - or first give yourself elevated permissions on the /usr/local directory as documented [here](http://foohack.com/2010/08/intro-to-npm/#what_no_sudo)

```bash
npm install adapt-cli -g
npm install grunt-cli -g
```

### Get the Adapt output framework
#### Overview
The output framework is the generic codebase used to create e-learning content – in other words, it is the generic code that runs as part of the e-learning package in the user’s browser when working through an e-learning module based on Adapt. 

#### Downloading the framework
You can get the latest version of the framework from our [GitHub repository](/adaptlearning/adapt_framework) using the Adapt Command Line Interface.

First, open your command line utility and navigate to the folder where you'd like your Adapt course development files to be stored. Then run the command:

```bash
adapt create course
```

This will ask you to confirm four things:

1. type: accept the default (course)
1. name: change this if you want (or accept the default, you can always change it later if you need)
1. branch: accept the default (master)
1. create now?: accept the default (y)

A directory with the course name will be created and all the Adapt framework files will be downloaded into it. 

Alternatively you can [download](/adaptlearning/adapt_framework/archive/master.zip) it as a ZIP and perform a [manual installation](/adaptlearning/adapt_framework/wiki/Manual-installation-of-the-Adapt-framework).

The output framework contains all the source files and programs required to produce your course. The output framework uses [Grunt](http://gruntjs.com/) to manage the build process and run all of the grunt tasks from your output framework directory.

#### Building
In order to run the various build commands, you will need to navigate to the directory that was created when you ran the create course command earlier.

Assuming you used the default course name of 'my-adapt-course', you can change to that folder with the command:
```bash
cd my-adapt-course
```
You can then create a build of your course using:
```bash
grunt build
```
The build task compiles and compresses your course and prepares it for viewing and distribution. The output is located in the *build* directory.

#### Viewing the build
To view the build package create a local server:
```bash
grunt server
```

To emulate a SCORM server, use this command instead:
```bash
grunt server-scorm
```
Note: to terminate the server, press ctrl+c

This will now open your default browser at the following URL:
[http://localhost:9001/](http://localhost:9001/)

*N.B.* If you have run the server-scorm task, navigate to this URL to emulate an LMS environment:
[http://localhost:9001/main.html](http://localhost:9001/main.html)

This allows you to test your SCO without the need for a continual upload / update / reupload cycle. Please note that as this emulation uses an iframe, it is not suitable for device testing. It is intended for testing SCORM functionality only. If you do not require SCORM functionality, please run 

```bash
adapt uninstall contrib-spoor
grunt build
```
The server will display the default menu of the course in your browser with the view appropriate to the device you're using. Any changes to the course will automatically be built and displayed.

#### Building a course with different themes and menus
The theme and menu used in the build process can be customised using the `--theme` and `--menu` switches.  For example, if you had installed a new theme called `adapt-new-theme` and a new menu called `adapt-new-menu`, you could use them as follows:

````bash
grunt build --theme=adapt-new-theme --menu=adapt-new-menu
````


**Next** - [[Creating your first course]]