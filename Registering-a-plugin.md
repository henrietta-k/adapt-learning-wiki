All plugins are Bower packages; to create your plugin you will first need to define your package, and then register it with our plugin registry.

#### Registering a new plugin

To register a plugin, it must first comply with the following:
* There must be a valid manifest `bower.json` in the current working directory. 
* Your package must be available at a Git endpoint (e.g. `git://github.com/<user>/<repo_name>.git`).
* Your plugin repository should use [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) for releases.
* There must be a valid `.bowerrc` file in the current Git repository. See the [adapt_framework repository](https://github.com/adaptlearning/adapt_framework/blob/master/.bowerrc) for an example (you are fine to copy this as-is to your plugin source).

Once you are ready to publish, run the adapt command line interface and provide the required information.

```bash
$ adapt register
```

Your plugin will be published to the registry, you can confirm this by doing `adapt search <plugin-name>`. 

#### Plugin versioning

It is possible to maintain multiple versions of your plugin, giving you the freedom to change your plugin at any time without requiring existing users to migrate to newer versions. 
We strongly recommend that you follow [Semantic version numbers](//github.com/adaptlearning/adapt_framework/wiki/Semantic-Version-numbers) for your releases.

To create a new version of a registered plugin, simple [tag your git repository](http://git-scm.com/book/en/Git-Basics-Tagging) with the new version number.

To install a specific version of a plugin using the [Adapt Command Line Interface](//github.com/adaptlearning/adapt_framework/wiki/Adapt-Command-Line-Interface) run the install command followed by the name of the plugin, # symbol and then the version number.

For example, the following would install version `0.0.2` of the `adapt-hello-world` plugin:
```bash
adapt install hello-world#0.0.2
```