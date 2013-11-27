### Overview
The Adapt output framework has been designed to use a modular system of plugins. These plugins perform various  functions and allow you to pick and choose what components, extensions, themes and menus are used in your course.

The Adapt ecosystem of plugins is growing and allows developers to produce their own custom interactions and make them available to other. The plugin system is build on top of [Bower](http://bower.io/) and uses standard Bower packages alongside Git to create a searchable, shareable and distributed dependency model.
Each plugin must define itself as an [AMD module](https://github.com/amdjs/amdjs-api/wiki/AMD).

### Configuration
The Adapt output framework is pre-configured to search for plugins in our own registry, `http://adapt-bower-repository.herokuapp.com`.

### Creating a new plugin
All plugins are [Bower packages](http://bower.io/#defining-a-package); to create your plugin you will need to define your package and then register it with our plugin registry.

