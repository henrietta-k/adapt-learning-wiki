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

Adapt also allows modules to plugin into events through events triggered by core views. These events can be listened to by using the following syntax:

````
Adapt.on('pageView:postRender', function(view) {
    // 'view' is the current view triggering the event
})
````

Below is a list of all the core view events:
##### Core Events
* ('app:dataReady') - Triggered when all the course data is loaded.
* ('adapt:initialize') - Triggered when adapt is ready to start the router.
* ('router:menu', [currentModel]) - Triggered when a route hits a menu.
* ('router:page', [currentModel]) - Triggered when a route hits a page.
* ('remove') - Is used by Adapt to trigger an event to remove all views.
* ('device:resize', [Adapt.device.screenWidth]) - Triggered when the window resizes.
* ('device:changed', [Adapt.device.screenSize]) - Triggered when the device size changes.
##### Core Views
* ('menuView:preRender', [currentView]) - Triggered when a menuView has initialized.
* ('menuView:postRender', [currentView]) - Triggered when a menuView has rendered.
* ('pageView:preRender', [currentView]) - Triggered when a pageView has initialized.
* ('pageView:postRender', [currentView]) - Triggered when a pageView has rendered.
* ('pageView:ready', [currentView]) - Triggered when all the assets are loaded for a page.
* ('articleView:preRender', [currentView]) - Triggered when a articleView has initialized.
* ('articleView:postRender', [currentView]) - Triggered when a articleView has rendered.
* ('blockView:preRender', [currentView]) - Triggered when a blockView has initialized.
* ('blockView:postRender', [currentView]) - Triggered when a blockView has rendered.
* ('componentView:preRender', [currentView]) - Triggered when a componentView has initialized.
* ('componentView:postRender', [currentView]) - Triggered when a componentView has rendered.
* ('navigationView:preRender', [navigationView]) - Triggered when the navigationView has initialized.
* ('navigationView:postRender', [navigationView]) - Triggered when the navigationView has rendered.
* ('questionView:showFeedback', [feedback]) - Triggered when a question shows feedback.

##### Navigation Events
* ('navigation:menu') - Triggered when the menu button is pressed.