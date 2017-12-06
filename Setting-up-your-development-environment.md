### Before you begin
Installing Adapt requires the use of the [command line](https://en.wikipedia.org/wiki/Command-line_interface). If your skills are a little rusty, the wiki article [*Just Enough Command Line for Installing*](https://github.com/adaptlearning/adapt_authoring/wiki/Just-Enough-Command-Line-for-Installing) might be all the assistance you need. 

If you've never used the command line before, please take advantage of one of the many tutorials you'll find on the web. 

Adapt does not require you to be an expert with the command line, just familiar with basic terminology and techniques.  

### Prerequisites
Before you get started with Adapt, you will need to install [Node.js](http://nodejs.org/) (the LTS version) and [Git](http://git-scm.com/downloads) if you haven't already done so.

> Linux users please note that on some distributions the node folder is called 'nodejs' - which will not work. You can work around this by either running `$ apt install nodejs-legacy` or by creating a symbolic link that has the right name by doing something like `$ sudo ln -s /usr/bin/nodejs /usr/bin/node`

> Windows users may prefer [Git for Windows](https://msysgit.github.io/) or [Github for Windows](http://windows.github.com/). **Important: if you install Git for Windows, you will need to reboot after installation even though it doesn't prompt you to do this**.

> Mac users running OS X 10.9 Mavericks (or better) should be able to install Git simply by trying to run the command 'git' in the Terminal. It should recognise what you are trying to do and prompt you to install the XCode Command Line Tools, which include Git. Note that if you installed the XCode Command Line Tools whilst running a previous version of macOS then you may need to update by running `$ sudo xcode-select --install`. Also check for any updates in the App Store.

Once you've got both Git and Node.js installed, the other components you'll need can be installed with the Node Package Manager - AKA [npm](https://npmjs.org/) - which **comes installed with Node.js**

To install the components, run the following two commands - which can be done via Terminal on OS X or on Windows via whatever command line utility was installed when you installed Git e.g. Git Bash or PoshGit.

> Mac users - you will need to either prefix the commands with 'sudo' - or first give yourself elevated permissions on the /usr/local directory as documented [here](http://foohack.com/2010/08/intro-to-npm/#what_no_sudo)

```bash
npm install adapt-cli -g
npm install grunt-cli -g
```

### The Adapt framework
#### Overview
The Adapt framework consists of three main parts:
1. The 'source' - the files you'll need to edit/work with, located in a folder called 'src'
1. A 'task runner' - called Grunt - which takes the 'source' files and compiles them into:
1. The 'build' - this folder contains the course that you will eventually upload to a [web server](https://en.wikipedia.org/wiki/Web_server) or [Learning Management System](https://en.wikipedia.org/wiki/Learning_management_system).

#### Getting the framework
Although you can [download and install the framework manually](/adaptlearning/adapt_framework/wiki/Manual-installation-of-the-Adapt-framework), the majority of users find that the easiest and most efficient method is to use the Adapt **C**ommand **L**ine **I**nterface (which you installed as part of the prerequisites).

First, open your command line utility and navigate to the folder where you'd like your Adapt course development files to be stored. Then run the command:

```bash
adapt create course
```

This will ask you to confirm four things:

1. **type:** accept the default (course)
1. **name:** change this if you want (or accept the default, you can always change it later if you need)
1. **branch:** accept the default (master)
1. **create now?:** accept the default (y)

A directory with the course name will be created and all the Adapt framework files will be downloaded into it. 

#### Building your course
First you will need to navigate to the directory that was created when you ran the `adapt create course` command earlier.

Assuming you used the default course name of 'my-adapt-course', you can change to that folder with the command:
```bash
cd my-adapt-course
```
You can then create a build of your course using:
```bash
grunt build
```
The build task compiles and compresses your course and prepares it for viewing and distribution. The output is located in the *build* directory.

Whilst you are working on your course, you should use:
```bash
grunt dev
```
This task will compile your files with 'sourcemapping' enabled so as to allow for debugging using your browser's developer tools. It will also watch for changes so every time you save a file it will automatically process it as necessary. To exit, press <kbd>CTRL+c</kbd>

> Note: as a general rule, you should run `grunt build` on your course when you want to make it 'production-ready' as this 'minifies' the code, making it quicker for end users to download, improving course start-up performance.

#### Viewing the build
To view the course in your browser you need to create a local server:
```bash
grunt server
```
This will open the course in your default browser at the URL [http://localhost:9001/](http://localhost:9001/)

> Running the course from a server ensures that it will load and run properly. If you were to run your course by double-clicking build/index.html your browser would almost certainly apply very strict 'local security' policies to it which would prevent it from working.

Note: to terminate the server, press <kbd>CTRL+c</kbd>

To emulate a [SCORM](https://scorm.com/scorm-explained/) server, use this command instead:
```bash
grunt server-scorm
```
This will open the course in your default browser at the URL [http://localhost:9001/scorm_test_harness.html](http://localhost:9001/scorm_test_harness.html) and will allow the course to mimic some of the SCORM 1.2 tracking behaviour that would normally only be available from an LMS. This allows you to test your SCO without the need for a continual upload / update / reupload cycle. Note that this is NOT a substitute for doing proper SCORM testing which should always be conducted on a real Learning Management System. If you do not have access to one you can [create an account on SCORM Cloud](https://cloud.scorm.com/sc/guest/SignUpForm) for free.

If you need to reset the stored data, open the browser console and execute the command `API.LMSClear()`.

If you do not require SCORM functionality, run 
```bash
adapt uninstall contrib-spoor
grunt build
```
To remove the SCORM tracking plugin completely.

#### Building a course with different themes and menus
The theme and menu used in the build process can be customised using the `--theme` and `--menu` switches.  For example, if you had installed a new theme called `adapt-new-theme` and a new menu called `adapt-new-menu`, you could use them as follows:

````bash
grunt build --theme=adapt-new-theme --menu=adapt-new-menu
````


**Next** - [[Creating your first course]]