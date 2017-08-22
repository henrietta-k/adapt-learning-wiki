### Overview
The Adapt output framework has been designed to use a modular system of plug-ins. These plug-ins perform various  functions and allow you to pick and choose what components, extensions, themes, and menus are used in your course.

The Adapt ecosystem of plug-ins is growing and allows developers to produce their own custom interactions and make them available to others. The plug-in system is built on top of [Bower](http://bower.io/) and uses standard Bower packages alongside Git to create a searchable, shareable and distributed dependency model.
Each plug-in must define itself as an [AMD module](/amdjs/amdjs-api/wiki/AMD).

### Configuration
The Adapt output framework is pre-configured to search for plug-ins in our own registry, `http://adapt-bower-repository.herokuapp.com`.

### Creating a new plug-in


#### Plug-in naming policy
In order to publish a plug-in it is required that a plug-in name must:-

1. Be **Unique**, plug-in names are available on a first come, first serve basis.
2. Start with **adapt-**
3. Not start with **adapt-contrib-**, this is reserved for plug-ins that have been acknowledged by the Adapt Community as "officially" supported. To achieve contrib status a plug-in must conform to the projects standard for code convention and test coverage.

#### Implementing a plug-in
The plug-ins JavaScript file must define itself as an AMD module (this is the file specified by the `main` property in your package)

```js
define([
    "core/js/adapt",
    "core/js/views/componentView"
], function(Adapt, ComponentView) {

    var MyPlugin = {
       // implement your component
    };
    return MyPlugin;
   
});
```

If your plug-in has a user interface, then you can include [LESS](http://lesscss.org/) stylesheets (.less) and [Handlebars](http://handlebarsjs.com/) templates (.hbs).
These files will be compiled and included in the course output.

#### Organizing plug-in files
Plug-ins will often include several types of files. Storing these in following named folders ensures they will be copied to the proper location by the `grunt build` process.   

| plug-in folder | file description |  course output location |
| ---- | ---- | ---- | 
| `/js` | JavaScript files | `/adapt/js/adapt.min.js` |  
| `/less` | Less file used to style the plug-in | `/adapt/css/adapt.css` |
| `/templates` | Handlebars (`.hbs`) files used to create the plug-in views | `/templates.js` |
| `/assets` | Graphic and media files | `/assets/` for components and extensions, `/adapt/css/assets/` for themes|
| `/libraries` | JavaScript libraries from third-parties and the like that are referenced by the plug-in's js file. | `/libraries/`  |
| `/required` | Any additional files to go in the course 'root' folder e.g. SCORM manifest files | `/` |
| `/scripts` | Compile time scripts | n/a |


#### Defining a package
All plug-ins are [Bower packages](http://bower.io); to create your plug-in you will need to define your package and then register it with our plug-in registry. If you need to install Bower first, you can do so with the following command:

```
npm install -g bower
```

You must create a `bower.json` in your plug-in's root, and specify all of its dependencies. This is similar to Node's `package.json`, or Ruby's `Gemfile`, and is useful for locking down a project's dependencies.

You can interactively create a `bower.json` with the following command:

```
bower init
```

The `bower.json` defines several options:

* `name` [string, required]: The name of your package.
* `version` [string]: A semantic version number (see [semver](http://semver.org/)).
* `framework` [string]: The semantic version(s) of the Adapt framework that your package works with. This can be a single version (e.g. `2.0.0`), a range of versions (e.g. `>2.0.0`) or multiple discreet versions (e.g. `2.0.1 || 2.0.3). (see [Semver Ranges](https://nodesource.com/blog/semver-a-primer#semver-ranges)).
* `main` [string, required]: The main javascript AMD module for your package.
* `repository` [string]: The git repository where the package is available.
* `keywords` [array]: An array containing one of the following values, `adapt-component`, `adapt-extension`, `adapt-menu` or `adapt-theme`
* `ignore` [array]: An array of paths not needed in production that you want Bower to ignore when installing your package.
* `dependencies` [hash]: Packages your package depends upon in production. (unsupported)
* `devDependencies` [hash]: Development dependencies.
* `private` [boolean]: Set to true if you want to keep the package private and do not want to register the package in future.
* `scripts` [hash]: Scripts to run at compile time. ``adaptpostbuild`` is the only supported hook.

```js
{
  "name": "adapt-hello-world",
  "version": "0.0.4",
  "repository": "git://github.com/cajones/adapt-hello-world.git",
  "homepage": "https://github.com/cajones/adapt-hello-world",
  "authors": [
    "Chris Jones <chris.jones@spongeuk.com>"
  ],
  "description": "a really simple adapt plugin",
  "main": "/js/helloWorld.js",
  "keywords": [
    "adapt-component"
  ],
  "scripts": {
    "adaptpostbuild": "/scripts/postbuild.js"
  },
  "license": "GPLv3"
}
```

#### Scripts
All compile time scripts should take this form:
```javascript
//src/extensions/adapt-extensionName/scripts/postbuild.js
module.exports = function(fs, path, log, options, done) {
    /* where
    options = {
        sourcedir: "/path/to/root/src",
        outputdir: "/path/to/root/build",
        plugindir: "/path/to/root/src/extension/adapt-extensionName"
    };
   */
   log(JSON.stringify(options, null, 4));
   done();
};
```
To control the execution of scripts you can add the following to the ``config.json``:
```json
"build": {
  "scriptSafe": "adapt-contrib-xapi, adapt-extensionName"
}
```
To execute all scripts without modifying the ``config.json``:
```
grunt dev --allowscripts
grunt build --allowscripts
```

**Next** - [Registering a plug-in](https://github.com/adaptlearning/adapt_framework/wiki/Registering-a-plugin)