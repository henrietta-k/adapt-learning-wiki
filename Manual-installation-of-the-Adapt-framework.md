## Introduction  
The [Adapt-CLI](/adaptlearning/adapt_framework/wiki/Adapt Command Line Interface) provides a command for creating a course. The command downloads and installs the latest public release of the Adapt framework. It is the easiest way for a developer/author to [set up a development environment](https://github.com/adaptlearning/adapt_framework/wiki/Setting-up-your-development-environment#installation).

There may be times when using the command line interface is unsuitable, for example, when installing the develop branch or when installing a fork or test package. Such situations require manual installation, and the following instructions aim to help.  

##Installation Overview
1. **<a href="#1">Install prerequisites.</a>**  
Installation of the Adapt framework depends on Node, Git, Grunt, and the Adapt-CLI.

2. **<a href="#2">Download the framework.</a>**  
Download the source code from its repository on GitHub.

3. **<a href="#3">Install module dependencies.</a>**  
Use `npm` and `adapt` to install required packages and plug-ins.

4. **<a href="#4">Run the application.</a>**  
Build the supplied sample course and start a server.

____________


##<a name="1"></a>1. Install Prerequisites

Install the following before proceeding:
* <a href="http://git-scm.com/downloads" target="_blank">Git</a>
* <a href="http://nodejs.org/" target="_blank">Node.js</a>
* <a href="http://gruntjs.com/" target="_blank">grunt-cli</a>
* <a href="https://github.com/adaptlearning/adapt-cli" target="_blank">adapt-cli</a>  

> **Tips:**  
> + To verify if a requirement is already installed, [check for its version.](https://github.com/adaptlearning/adapt_authoring/wiki/Just-Enough-Command-Line-for-Installing#check-version)  
> + Windows users should run these commands in Git Bash if Git was installed using default settings.
> + Mac and Linux users may need to prefix the commands with `sudo` or give yourself elevated permissions on the /usr/local directory as documented <a href="http://foohack.com/2010/08/intro-to-npm/#what_no_sudo" target="_blank">here</a>.

##<a name="2"></a>2. Download the Framework.

Download the Adapt framework as a ZIP and extract the files. (If you are a Windows user, you may need to <a href="http://answers.microsoft.com/en-us/windows/forum/windows_7-security/windows-found-that-this-file-is-potentially/cab2b576-2074-4b26-bf54-571fe03f9ef8" target="_blank">unblock the ZIP archive</a> before you extract it.)

Open a console interface (e.g. Git Bash, Terminal on OSX, Powershell or CMD.exe) and navigate to the extracted folder (typically adapt_framework-master, but you can safely rename this). 

##<a name="3"></a>3. Install Module Dependencies.  

With the extracted folder as your current working directory, run the following command.     
`npm install`  

This will install all of the package dependencies of the framework. Be patient. If any error occurs, read the output. Determine if a dependency failed to install properly, if you forgot to install one of the prerequisites, or if you require elevated permissions. If you need assistance troubleshooting, consult the Adapt community's [Technical Discussion Forum](https://community.adaptlearning.org/mod/forum/view.php?id=4). If this command completes successfully, run the following command.  
`adapt install`  

This will download all of the Adapt plug-ins to the correct locations in the framework.

##<a name="4"></a>4. Run the Application 

Build the included sample course by running the following command:  
`grunt build`  

Start a server by running the following command:   
`grunt server`  

To view the course, open a browser to the following URL:
[http://localhost:9001/](http://localhost:9001/)   
To terminate the server, press ctrl+c .  
