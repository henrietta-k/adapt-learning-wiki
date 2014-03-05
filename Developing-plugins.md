### Overview
The Adapt output framework has been designed to use a modular system of plugins. These plugins perform various  functions and allow you to pick and choose what components, extensions, themes and menus are used in your course.

The Adapt ecosystem of plugins is growing and allows developers to produce their own custom interactions and make them available to others. The plugin system is built on top of [Bower](http://bower.io/) and uses standard Bower packages alongside Git to create a searchable, shareable and distributed dependency model.
Each plugin must define itself as an [AMD module](https://github.com/amdjs/amdjs-api/wiki/AMD).

### Configuration
The Adapt output framework is pre-configured to search for plugins in our own registry, `http://adapt-bower-repository.herokuapp.com`.

### Creating a new plugin
All plugins are [Bower packages](http://bower.io/#defining-a-package); to create your plugin you will need to define your package and then register it with our plugin registry.
##### Defining a package
You must create a `bower.json` in your plugin's root, and specify all of its dependencies. This is similar to Node's `package.json`, or Ruby's `Gemfile`, and is useful for locking down a project's dependencies.

You can interactively create a `bower.json` with the following command:

```
bower init
```

The `bower.json` defines several options:

* `name` [string, required]: The name of your package.
* `version`: A semantic version number (see [semver](http://semver.org/)).
* `main` [string, required]: The main javascript AMD module for your package.
* `repository` [string]: The git repository where the package is available.
* `keywords` [array]: An array containing one of the following values, `adapt-component`, `adapt-extension`, `adapt-menu` or `adapt-theme`
* `ignore` [array]: An array of paths not needed in production that you want Bower to ignore when installing your package.
* `dependencies` [hash]: Packages your package depends upon in production.
* `devDependencies` [hash]: Development dependencies.
* `private` [boolean]: Set to true if you want to keep the package private and do not want to register the package in future.

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
  "license": "GPLv3"
}
```
###### Plugin naming policy
In order to publish a plugin it is required that a plugin name must:-

1. Be **Unique**, plugin names are available on a first come, first serve basis.
2. Start with **adapt-**
3. Not start with **adapt-contrib-**, this is reserved for plugins that have been acknowledged by the Adapt Community as "offically" supported. To achieve contrib status a plugin must conform to the projects standard for code convention and test coverage.

##### Implementing a plugin
The javascript file that is specified by the `main` property must define itself as an AMD module.

```js
define(["coreViews/componentView", "coreJS/adapt"], function(ComponentView, Adapt) {

    var MyPlugin = {
       // implement your component
    };        
    return MyPlugin;
   
});
```

If your plugin has a user interface then you can include [LESS](http://lesscss.org/) stylesheets (.less) and [Handlebars](http://handlebarsjs.com/) templates (.hbs).
These files will be compiled and included in the course output.

##### Registering a plugin
To register a new package:

* There must be a valid manifest `bower.json` in the current working directory. 
* Your plugin version should use server Git tags.
* Your package must be available at a Git endpoint (e.g. git://GitHub.com/....git)

Once you are ready to publish, run the adapt command line interface and provide the required information.

```bash
$ adapt register
```

Your plugin will be published into the registry, you can confirm this by doing `adapt search <plugin-name>`. 

**Next** - 