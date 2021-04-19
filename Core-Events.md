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

### Adapt built-in events

Adapt also allows modules to plugin into events through events triggered by core views. These events can be listened to by using the following syntax:

````
Adapt.on('pageView:postRender', function(view) {
    // 'view' is the current view triggering the event
});
````

#### Core events

Event | Argument | Description
----- | -------- | -----------
`configModel:dataLoaded` | | Triggered when the config model is loaded. This can be used to stop the course files from being fetched.
`configModel:loadCourseData` | | Triggered just before Adapt creates the main content collections and models. This can be used to load the course files if a plugin has stopped the default fetch.
`app:dataLoaded` || Triggered when all the JSON is loaded, triggers adaptModel to start setting up all the contentObject/article/block/component/sibling/ancestor/children/parent mappings
`app:dataReady` | | Triggered when all the course data is loaded AND all the models/mappings have been setup.
`app:languageChanged` | `newLanguage` | Triggered if the user changes the course language. The argument `newLanguage` will be set to the language code of the new language e.g. `"fr"` for French. Changing language will trigger a reload of all the course content and a re-render of the course itself so components, menus and themes should get updated automatically - but some extensions (e.g. resources, glossary, spoor) will need to do extra work when the language is changed.
`adapt:start` | | Triggered before Adapt starts the router, gives the start controller an opportunity to set a custom start location.
`adapt:initialize` | | Triggered when Adapt is ready to start the router.
`router:location` | `Adapt.location` | Triggered when the location changes.
`router:menu` | `model` | Triggered when a route hits a menu.
`router:page` | `model` | Triggered when a route hits a page.
`remove` | | Is used by Adapt to trigger an event to remove all views.
`preRemove` | | Is used by Adapt to trigger an event that must occur immediately prior to `remove`.
`postRemove` | | Is used by Adapt to trigger an event that must occur immediately after `remove`.
`device:resize` | `Adapt.device.screenWidth` | Triggered when the window resizes.
`device:changed` | `Adapt.device.screenSize` | Triggered when the device size changes.

#### Core views

##### Generic Events
These events are triggered by all the different view types in Adapt - so you can listen to the event from a specific kind of view by changing `view:` to one of the following:
* `contentObjectView:` (pages and menus)
* `menuView:`
* `pageView:`
* `articleView:`
* `blockView:`
* `componentView:`

Event | Argument | Trigger
----- | -------- | -----------
`view:preRender` | `view` | a view has initialised
`view:render` | `view` | a view is rendering
`view:postRender` | `view` |  a view has rendered
`view:preRemove` | `view` | a view about to be removed
`view:remove` | `view` | a view is being removed
`view:postRemove` | `view` | a view has been removed


##### Page/Menu Events
These events are all triggered by page or menu views - so you can listen to the event from a specific kind of view by changing `view:` to one of the following:
* `contentObjectView:` (pages and menus)
* `menuView:`
* `pageView:`

Event | Argument | Trigger
----- | -------- | -----------
`view:preReady` | `view` | a view is about to start loading its assets
`view:ready` | `view` | all the view's assets have loaded
`view:postReady` | `view` | all the assets are loaded for a view

##### Navigation events
Event | Argument | Trigger
----- | -------- | -----------
`navigationView:preRender` | `view` | navigation view has initialised
`navigationView:postRender` | `view` | navigation view has rendered
`navigation:backButton` | `null` | the navigation back button is pressed
`navigation:homeButton` | `null` | the navigation home button is pressed
`navigation:parentButton` | `null` | the navigation up button is pressed
`navigation:skipNavigation` | `null` | the skip navigation button is pressed
`navigation:returnToStart` | `null` | the return to start button is pressed
`navigation:toggleDrawer` | `null` | the drawer toggle button is clicked


##### Question events
Event | Argument | Trigger
----- | -------- | -----------
`questionView:showFeedback` | `view` | a question shows feedback. Question view automatically sets up `feedbackTitle` and `feedbackMessage` as attributes on the current view’s model
`questionView:disabledFeedback` | `view` | a question is meant to show feedback but `_canShowFeedback` is disabled on the model
`questionView:showInstructionError` | `view` | the learner has pressed submit without having selected an answer
`questionView:recordInteraction` | `view` | the learner has answered a question that needs to be reported to SCORM/xAPI's cmi.interactions
`question:refresh` | `null` | add desc
`buttons:stateUpdate` | `BUTTON_STATE` | one of the buttons in the question buttons view has been pressed. The argument `BUTTON_STATE` is an [enum](https://en.wikipedia.org/wiki/Enumerated_type) representing the state of the button at the time it was pressed e.g. `BUTTON_STATE.SHOW_CORRECT_ANSWER` if the 'Show Correct Answer' button was pressed, `BUTTON_STATE.HIDE_CORRECT_ANSWER` if the 'Show your answer' button was pressed.