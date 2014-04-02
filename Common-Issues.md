## Installation/Setup
### 'Can't stat' error when creating a course
On Windows, when running ```adapt create course``` you receive an error similar to:
```
Oh dear, something went wrong. I'm terribly sorry.
Can't stat "Users\\your.username\\.adapt\\tmp\\50233e50-b8e7-11e3-b613-9343b13d4c4c\\adapt_framework-master\\.bowerrc": Error: ENOENT, stat 'C:\Users\your.username\Documents\Adapt\Users\your.username\.adapt\tmp\50233e50-b8e7-11e3-b613-9343b13d4c4c\adapt_framework-master\.bowerrc'
```
To fix this, you'll need to configure your $HOME environment variable.

On Win 7 go to Control Panel\All Control Panel Items\System then select Advanced system settings > Environment variables 

Then add a new variable called HOME with the value 'C:\Users\your.username\' (or whatever the correct path to your user profile directory happens to be)