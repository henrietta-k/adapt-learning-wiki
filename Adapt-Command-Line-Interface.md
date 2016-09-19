**Important**: the CLI is only for use with developing *standalone* courses using the framework. Please do not attempt to use it in conjunction with an authoring tool installation.

---
The Adapt command-line interface (CLI) is a set of cross platform command-line tools for developers to create, manage and build Adapt courses and plugin.

Check out the CLI's [README](https://github.com/adaptlearning/adapt-cli) for full details.

### Installation

**Prerequisites**: NodeJS (and NPM)

To install the Adapt CLI, run the following from the command line:
```bash
$ npm install adapt-cli -g
```
This will install the CLI globally (i.e. allow you to access the tools from anywhere on your computer).

### Update
To update the Adapt CLI run the following command
```bash
$ npm update adapt-cli -g
```

### CLI features
* Create courses
* Search for plugins
* Install a plugin
* Uninstall a plugin

##### Creating an Adapt course

    adapt create {type} {path} [{branch}]

type - What to create. Only the value "course" is currently supported. 
path - The directory of the new course.
branch - Optional - The branch of the framework to be downlaoded.

For example...

    adapt create course "My Course"

This will download the Adapt framework and create an new course in the directory "My Course", in your current directory.

##### Searching for an Adapt plugin.

    adapt search {name or partial name of plugin to search for}


##### Installing a plugin into your current directory

    adapt install {name of plugin}

Additionally you can install a specific version of a plugin.

    adapt install {name of plugin}#{version}

Anywhere that you are required to provide a name of a plugin it can be either fully qualified with 'adapt-' or optionally you can omit the prefix an just use the plugin name.

Therefore these commands are equivalent:

    adapt install adapt-my-plugin
    adapt install my-plugin

Installed plugins are saved to `adapt.json`. 

##### Installing plugins previously saved in adapt.json

    adapt install


##### Uninstalling a plugin from your current directory

    adapt uninstall {name of plugin}

The Plugin Registry
-------------------

The plugin system is powered by [Bower](http://bower.io/). Each plugin should be a valid bower package and they should be registered with the Adapt registry.

    http://adapt-bower-repository.herokuapp.com/packages/

See [Developing plugins](https://github.com/adaptlearning/adapt_framework/wiki/Developing-plugins) for more information on defining your plugins package.

##### Registering a plugin

From within a plugin directory

    adapt register

`name` and `repository` will be read from `bower.json` in the current directory.