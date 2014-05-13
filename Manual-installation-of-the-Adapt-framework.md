
### Overview
To manually install the Adapt framework you will first need to [download](/adaptlearning/adapt_framework/archive/master.zip) it as a ZIP and extract the files to your course folder.

If you are a Windows user you may additionally need to unblock the zip archive before you extract it.

Then from the course folder you can run ```npm install``` to download and install the framework dependencies, and ```adapt install``` to install the Adapt Core plugins.

### Requirements

Before you start, make sure that you have followed the initial steps in the [Setting up your development environment](/adapt_framework/wiki/Setting-up-your-development-environment#installation) guide.

You should then have [node.js](http://nodejs.org/), [git](http://git-scm.com/book/en/Getting-Started-Installing-Git), [Adapt Command Line Interface](/adaptlearning/adapt_framework/wiki/Adapt Command Line Interface) and [Grunt](http://gruntjs.com/getting-started) installed.

### Installation

[Download](/adaptlearning/adapt_framework/archive/master.zip) the framework as a ZIP and extract the files to your course folder. If you are a Windows user you may additionally need to unblock the zip archive before you extract it.

Open the course folder in a console interface (e.g. Git Bash, Terminal on OSX, Powershell or CMD.exe) and navigate to your course folder where you extracted the framework files.

Run 
```bash
npm install
```
This will install all of the dependencies of the framework and get Adapt up and running.

Next run 
```bash
adapt install
```
This will download all of the adapt plugins to the correct locations in this course folder.

Finally you can run  

```bash
grunt build
grunt server
```
This will build the default course and compile the source files ready for viewing.
