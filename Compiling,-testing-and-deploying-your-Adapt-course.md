**Important**: if using the authoring tool, please do not attempt to build individual courses using the below instructions (unless you *really* know what you're doing).

---

To make developing and deploying Adapt courses as painless as possible, we use the [Grunt task runner](http://gruntjs.com/) to automate as many of the menial tasks as possible.

## Tasks

After navigating to the root directory of your Adapt course (you know you're in the right place if you have a _Gruntfile.js_), you can run any of the grunt tasks by typing `grunt` followed by the task name:
<br/>For example,  
`grunt build`  

Below is a list of the available tasks. (For brevity, the `grunt` portion has been left out.)

| Task&nbsp;name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description |
| ---- | :---------- |
| `help` | Lists out all available tasks along with descriptions. Useful to quickly look up what's available without having to leave the command line. <br/>_**Tip**: Simply running_ `grunt` _will have the same effect._ |
| `build` | Compiles all files in `src` to create a production-ready minified/compressed version of your course. <br/>_**Extra info:** Each time you run_ `build`_, grunt does the following: checks the JSON for errors, copies all assets, compiles the Less, compiles the handlebars templates, generates dynamic configuration options (_ config.json _and_ course.json _), inserts any missing tracking IDs, and finally compiles the js. This explains why it can take a while sometimes!_ |
| `dev` | The same as `build`, with a few notable *developer-friendly* differences:<ul><li>Includes [source maps](http://blog.teamtreehouse.com/introduction-source-maps) for both the Javascript and Less.</li><li>Runs the `watch` task, which monitors your source code for any file changes and runs the appropriate grunt tasks to automatically update your build.</li></ul> |
| `check-json` | Validates the course JSON, checks for duplicate IDs, and checks that each element has a parent. <br/>_**Note**: This task runs during the_ `build` _and_ `dev` _tasks, so there is usually no need to run it manually._ |
| `tracking-insert` | Adds tracking identifiers to the relevant places in your JSON files. This task only fills in any missing IDs (any existing IDs are left), which can result in non-sequential numbering. If this bothers you, you can use `tracking-reset`.<br/>_**Note**: This task runs during the_ `build` _and_ `dev` _tasks, so there is usually no need to run it manually._ |
| `tracking-remove` | Removes all tracking IDs from your JSON files. Use this if you aren't using a tracking plug-in such as adapt-contrib-spoor. <br/> _**Note**: Leaving the IDs in has no detrimental effect._ |
| `tracking-reset` | Resets all tracking IDs in your JSON files starting from 0. |
| `server` | Runs a local server on your machine and opens a browser window ready for you to test your course locally. Check the console output for the URL. |
| `server-scorm` | Same as above but provides a dummy SCORM interface to allow you to test the tracking of your course. |
| `translate:export` | Exports translatable text from the master course. |
| `translate:import` | Imports translated text files and creates a new language version of the course. |

## Creating the SCORM package
Once you have built your course using `build` or `dev`, you are ready to upload it to a web server or LMS. To do this, you simply need to copy the files found in `/build` according to the instructions for your specific platform.