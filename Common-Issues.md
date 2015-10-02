## Installation/setup
###'Can't find Python executable' error when installing Adapt
On Windows, when running ```$ npm install adapt-cli -g```, you receive a long list of errors and the first few are something like:
```
gyp ERR! configure error
gyp ERR! stack Error: Can't find Python executable "python", you can set the PYTHON env variable.
```
You should just reboot your PC to allow the environment variables to be set correctly, the try the command again. You may still get an error like 'optional dep failed, continuing' - that's OK because it's only an option dependency.

###'git is not installed' error when installing Adapt
On Windows, when running ```$ npm install adapt-cli -g```, you receive an error like:
```
Oh dear, something went wrong. I'm terribly sorry. git is not installed or is not in the path
```
To fix this, check that GIT is installed correctly and add GIT to your system path, as documented at http://blog.countableset.ch/2012/06/07/adding-git-to-windows-7-path/
### 'fatal: unable to connect to github.com'
The likely problem here is that cloning from GitHub using the `git://` protocol has been blocked by a firewall. Check [this helpful answer](http://stackoverflow.com/questions/4891527/git-protocol-blocked-by-company-how-can-i-get-around-that) on StackOverflow for a troubleshooting guide.

## Course creation
### 'Can't stat' error when creating a course
On Windows, when running ```$ adapt create course``` you receive an error similar to:
```
Oh dear, something went wrong. I'm terribly sorry.
Can't stat "Users\\your.username\\.adapt\\tmp\\50233e50-b8e7-11e3-b613-9343b13d4c4c\\adapt_framework-master\\.bowerrc": Error: ENOENT, stat 'C:\Users\your.username\Documents\Adapt\Users\your.username\.adapt\tmp\50233e50-b8e7-11e3-b613-9343b13d4c4c\adapt_framework-master\.bowerrc'
```
To fix this, you'll need to configure your $HOME environment variable.

On Win 7 go to Control Panel\All Control Panel Items\System then select Advanced system settings > Environment variables 

Then add a new variable called HOME with the value 'C:\Users\your.username\' (or whatever the correct path to your user profile directory happens to be)