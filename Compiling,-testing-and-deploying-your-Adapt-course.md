To make developing and deploying Adapt courses as painless as possible, we use the [Grunt task runner](http://gruntjs.com/) to automate the as many of the menial tasks as possible.

## Tasks

After navigating to the root directory of your Adapt course (you know you're in the right place if you have a Gruntfile.js), you can any of the grunt tasks by typing `grunt` followed by the task name:
<br/>e.g. 
```javascript
grunt build
```
See below for a list of the available tasks (for brevity, the `grunt` portion has been left out):

| Task&nbsp;name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description |
| ---- | :---------- |
| `help` | Lists out all available tasks along with descriptions. Useful to quickly look up what's available without having to leave the command line. <br/>_**Tip**: simply running `grunt` will have the same effect._ |
| `build` | Compiles all files in `src` to create a production-ready minified/compressed version of your course. <br/>_**Extra info:** each time you run build, we do the following: check the JSON for errors, copy all assets, compile the less, compile the handlebars templates, generate dynamic configuration options (config.json & course.json), insert any missing tracking ids and finally compile the js. This explains why it can take a while sometimes!_ |
| `dev` | The same as `build`, with a few notable *developer-friendly* differences:<ul><li>Includes [source maps](http://blog.teamtreehouse.com/introduction-source-maps) for both the Javascript and LESS.</li><li>Runs the `watch` task, which monitors your source code for any file changes, and runs the appropriate grunt tasks to automatically update your build.</li></ul> |
| `check-json` | Validates the course JSON, checks for duplicate IDs, and that each element has a parent. <br/>_**Note**: this task runs during the `build` and `dev` tasks, so there is usually no need to run it manually._ |
| `tracking-insert` | Adds tracking identifiers to the relevent places in your JSON files. This task only fills in any missing IDs (any existing IDs are left), which can result in non-sequential numbering. If this bothers you, you can use `tracking-reset`.<br/>_**Note**: this task runs during the `build` and `dev` tasks, so there is usually no need to run it manually._ |
| `tracking-remove` | Removes all tracking IDs from your JSON files. Use this if you aren't using a tracking plugin. <br/> _**Note**: leaving the IDs in has no detrimental effect._ |
| `tracking-reset` | Resets all tracking IDs in your JSON files starting from 0. |
| `server` | Runs a local server on your machine and opens a browser window ready for you to test your course locally. Check the output for the URL. |
| `server-scorm` | Same as above, but provides a dummy SCORM interface to allow you to test the tracking of your course. |

## Creating the SCORM package
Once you have built your course using `build` or `dev`, you are ready to upload it to a web server or LMS. To do this, you simply need to copy the files found in `/build` according to the instructions for your specific platform.