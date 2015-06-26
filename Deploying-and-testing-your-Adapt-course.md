To make developing and deploying Adapt courses as painless as possible, we use the [Grunt task runner](http://gruntjs.com/) to automate the as many of the menial tasks as possible.

After navigating to the root directory of your Adapt course (you know you're in the right place if you have a Gruntfile.js), you can run any of the tasks below: 

#### `$ grunt`
Simply running this will list out all of the tasks along with descriptions; useful to quickly look up what's available without having to open your browser and navigate here.

#### `$ grunt build`
This tasks compiles a production-ready minified/compressed version of the course.

#### `$ grunt dev`
This tasks compiles a developer-friendly version of the course, including sourcemaps for debugging. Also runs the 'watch' task, which monitors your source code for any file changes, running the appropriate grunt tasks to update the build.

#### `$ grunt tracking-insert`
Before your course will track to an LMS (using [spoor](https://github.com/adaptlearning/adapt-contrib-spoor) or another tracking extension), you'll need to make sure that tracking identifiers are added to the relevant places in your JSON files. You _**can**_ do it manually, or you can run this task which will insert them for you automatically.

_**Note**: if you already have tracking IDs associated to blocks in your course, any missing IDs will be added starting from the highest existing ID (i.e. if the last block in your course has an ID of 17, the next ID added will be 18). If you want to remove all IDs, and start again from 0, try using `tracking-reset` (see below)._

#### `$ grunt tracking-remove`
This task removes all tracking IDs from your JSON files.

#### `$ grunt tracking-reset`
This task resets all tracking IDs in your JSON files starting from 0.

#### `$ grunt server`
This task runs a local server on your machine, and opens a browser window ready for you to test your course locally.

#### `$ grunt server-scorm`
Same as above, but provides a dummy SCORM interface to allow you to test the tracking of your course.

## Creating the SCORM package
Once you have built your course using `build` or `dev`, you are ready to upload it to a web server or LMS. To do this, you simply need to copy the files found in `/build` according to the instructions for your specific platform.