### AdaptModel

All core models inherit from AdaptModel (adaptModel.js) and contain the following methods:

##### - <a name="getChildren"></a>getChildren()

Returns the current models children as a collection.

````
var myChildren = Adapt.articles[0].getChildren();
// returns the article's blocks as a collection.
````

##### - <a name="getParent"></a>getParent()

Returns the current models parent as a model.

````
var myParent = Adapt.articles[0].getParent();
// returns the article's page model.
````

##### - <a name="getSiblings"></a>getSiblings()

Returns a collection of all the current models siblings.

````
var mySiblings = Adapt.blocks[0].getSiblings();
// returns all the blocks in the same article as the first block.
````

##### - <a name="findAncestor"></a>findAncestor(ancestors)

Finds ancestors of the current model and returns a model. Because of the way our menus system is setup findAncestor only works from components up to page level

````
var currentPage = Adapt.components[0].findAncestor('pages');
// returns the current page model that is an ancestor of the first component.
````

##### - <a name="findDescendants"></a>findDescendants(descendants)

Finds descendants of the current model and returns a collection. Like findAncestor this only works from page level down to components.

````
var children = Adapt.pages[0].findDescendants('components');
// returns all the components that are in the first page.
````

##### - <a name="setOnChildren"></a>setOnChildren(key, value, [options])

Sets attributes on all children models. An object can also be passed in to allow multiple attributes to be set at once. The standard Backbone options can also be passed in.

````
var firstPage = Adapt.pages[0];
firstPage.setOnChildren('_complete', true);
// sets all childrens '_complete' attribute to true, all the way down to component level.

firstPage.setOnChildren({'_complete': false, 'title', 'I have a new title'});
// Uses an object to set all childrens '_complete' attribute to false and 'title' attribute to 'I have a new title'.

firstPage.setOnChildren('_complete', true, {silent:true});
> or
firstPage.setOnChildren({_complete:true}, {silent:true});
// Passes an option of silent:true so the models will not fire off a change event.
````

### AdaptView

All core views inherit from AdaptView (adaptView.js) and contain the following methods:

##### - <a name="adapt-view-initialize"></a>initialize()

This is called when a view is created. This should never be overwritten as it sets up each view to work with Adapt. It follows the structure below:

* Set model to not ready - used when finding out whether a page is ready to display after all assets are downloaded.
* Listen to Adapt for any 'remove' events and remove this view.
* Call this.init() - used to setup anything on the view or model before rendering.
* Trigger 'preRender' event based upon the views type - 'pageView:preRender' - this is used by plugins to tap into a view before render.
* Call this.render() - renders the view into the dom.
* Trigger 'postRender' event based upon the views type - 'pageView:postRender' - this is used by plugins to tap into a view after render.
* Call this.postRender() - used to setup anything on the view or model after rendering.

##### - <a name="adapt-view-init"></a>init()

##### - <a name="adapt-view-render"></a>render()

##### - <a name="adapt-view-postRender"></a>postRender()

##### - <a name="adapt-view-setReadyListener"></a>setReadyListener()

##### - <a name="adapt-view-setCompletionListener"></a>setCompletionListener()

### Adapt.course

Adapt's main course object can be accessed by using:

````
Adapt.course
````

As this is inherited from AdaptModel you can call the following methods

[getChildren()](#getChildren)

[getParent()](#getParent)

[getSiblings()](#getSiblings)

[findAncestor(ancestors)](#findAncestor)

[findDescendants(descendants)](#findDescendants)

[setOnChildren(key, value, [options])](#setOnChildren)

### Events

To tap into our internal event system you would need to require 'coreJS/adapt' and use the following methods.

#####- trigger 
Triggers a global event.

#####- on 
Listens to a global event and calls a callback when triggered.

#####- off 
Removes the callback from an object.

#####- once
Similar to **on** but the callback is only fired once.

#####- listenTo
This is used to listen to an event on another object. If the object is removed at anytime during Adapt running, listenTo should be used as these events are stored and removed when a view is removed.

#####- stopListening
Stops listening to events on other objects so the callbacks will not be called.

#####- listenToOnce
Similar to listenTo but only calls the callback once.

#### A basic events implementation

    define(['coreJS/adapt'], function(Adapt) {
        
        Adapt.on('pluginName:changed', function() {
            console.log('callback fired');
        });

        Adapt.trigger('pluginName:changed');
        // output - 'callback fired'
 
        Adapt.off('pluginName:changed');

        Adapt.trigger('pluginName:changed');
        // output - no callback fired as event was removed with 'off'
        
        var View = new Backbone.View.extend({

            initialize: function() {
                this.listenTo(Adapt, 'pluginName:updated', this.callbackFromEvent);
                this.listenToOnce(Adapt, 'pluginName:stopListening', this.stopListeningToEvent);
            },

            callbackFromEvent: function() {
                console.log('listenTo callback fired');
            },

            stopListeningToEvent: function() {
                this.stopListening(Adapt, 'pluginName:updated');
            }

        });

        Adapt.trigger('pluginName:updated');
        // output - 'listenTo callback fired'

        Adapt.trigger('pluginName:stopListening');
        // output - calls the View.stopListeningToEvent method only once and removes the callback once fired

        Adapt.trigger('pluginName:updated');
        // output - nothing is called as the last event has remove the callback

    });

More information on our internal events system can be viewed [here](http://backbonejs.org/#Events)