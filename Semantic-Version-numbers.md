#### MAJOR.MINOR.PATCH
Semantic Versioning uses a three-part version number. The **major** version is incremented for big changes to the API which are not backward-compatible, the **minor** number is incremented for releases which add new (but crucially, **backward-compatible**) API features, and the **patch** number is incremented for minor changes and bug fixes which do not change the software's API.

#### Example scenario

- A plugin's first major release should have a version number of: **`1.0.0`**
- A subsequent bug-fix should bump the patch version number, resulting in **`1.0.1`**
- A new _backward-compatible_ feature is added, so the minor version is incremented: **`1.1.0`** (note that the patch number is reset to `0`) 
- Another bug-fix is added, changing the version to: **`1.1.1`**
- Some breaking changes are introduced, so the major version is incremented, and the minor and patch numbers are reset: **`2.0.0`**

#### More information

If you want to know more about semantic versioning, check out [this page](http://semver.org/) written by [@mojombo](https://github.com/mojombo).