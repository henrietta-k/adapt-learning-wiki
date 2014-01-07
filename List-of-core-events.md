### Overview

Adapt has been built with a module approach and to keep modules separate Adapt uses events to pass information between modules and notify them of changes.

### Backbone built-in events

To listen to changes on any core model use the Adapt collections or course model. Backbone automatically triggers an event when an attribute changes.

````
// List of collections
Adapt.contentObjects
Adapt.articles
Adapt.blocks
Adapt.components

// Course model
Adapt.course

// How to listen
Adapt.articles.on('change:_isComplete', function(model) {
    console.log('This article just changed complete status', model.get('_id'));
})

// If inside a view you can use listenTo
this.listenTo(Adapt.components, 'change', this.componentChangedAttribute);

// The model is passed into the componentChangedAttribute on the view
// Using 'change' listens to all changes on a model 
````

