All plugins are Bower packages; to create your plugin you will need to define your package and then register it with our plugin registry.

To register a new plugin:

* There must be a valid manifest `bower.json` in the current working directory. 
* Your plugin version should use server Git tags.
* Your package must be available at a Git endpoint (e.g. git://GitHub.com/....git)
* There must be a valid `.bowerrc` file in the current git repository - this can be taken from the adapt_framework repository.

Example:
```js
{
    "registry"  : "http://adapt-bower-repository.herokuapp.com/"
}
```

Once you are ready to publish, run the adapt command line interface and provide the required information.

```bash
$ adapt register
```

Your plugin will be published into the registry, you can confirm this by doing `adapt search <plugin-name>`. 

### Plugin versions
It is possible to maintain multiple version of your plugin, this give you the freedom to change you plugin at any time but still allow existing users migrate to newer versions at their leisure. 
We strongly recommend that you follow [Semantic version numbers](//github.com/adaptlearning/adapt_framework/wiki/Semantic-Version-numbers) for your releases.

To create a new version of a registered plugin, simple [tag your git repository](http://git-scm.com/book/en/Git-Basics-Tagging) with the version number.

To install a specific version of a plugin using the [Adapt Command Line Interface](//github.com/adaptlearning/adapt_framework/wiki/Adapt-Command-Line-Interface) run the install command followed by the name of the plugin, # symbol and then the version number.

```bash
adapt install hello-world#0.0.2
```

Would for example, install the adapt-hello-world plugin version 0.0.2.