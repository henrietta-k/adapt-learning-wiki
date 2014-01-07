### Overview

Adapt has been built with a module approach and to keep modules separate Adapt uses events to pass information between modules and notify them of changes.

### Backbone built-in events

To listen to changes on any core model use the Adapt collections. Backbone automatically triggers an event when an attribute changes.

````
// List of collections
Adapt.contentObjects
Adapt.articles
Adapt.blocks
Adapt.components
````

