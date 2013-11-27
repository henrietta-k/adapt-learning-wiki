## Overview
Adapt Command Line Interface is a set of cross platform command line tools for developers to create, manage and build Adapt courses and plugin.

Full details are available from the [NPM Package](https://npmjs.org/package/adapt-cli)

### Installation
To install the Adapt CLI, first be sure to install NodeJS, then from the command line run:-
```bash
npm install adapt-cli -g
```

### CLI features
* Search for plugins
* Install a plugin
* Uninstall a plugin

### Searching for plugins
Searching for an Adapt plugin.
```bash`
adapt search {name or partial name of plugin to search for}
```
### Installing plugins
Installing a plugin into your current directory
```bash
adapt install {name of plugin}
```
### Uninstalling plugins
Uninstalling a plugin from your current directory
```bash
adapt uninstall {name of plugin}
````
### Configuration
The plugin system is powered by Bower. Each plugin should be a [valid bower package](http://bower.io/#defining-a-package) and they should be registered with the Adapt registry `adapt-bower-repository.herokuapp.com`.