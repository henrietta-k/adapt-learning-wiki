Semantic Versioning uses a three-part version number: major version; minor version; and patch. The patch number is incremented for minor changes and bug fixes which do not change the software's API. The minor version is incremented for releases which add new, but backward-compatible, API features, and the major version is incremented for API changes which are not backward-compatible.

For example:-

Given I have a plugin on its first major release the version number would be *1.0.0*

When I release a bug fix then I should increment the patch, to be *1.0.1*

When I subsequently add a new feature that is backward-compatible I should increase the minor version, to be  *1.1.0* and reset the patch. 

When I release another bug fix to this new release then I should increment the patch, to be *1.1.1*

If I introduce breaking changes of my plugin then the major version should be incremented, *2.0.0*