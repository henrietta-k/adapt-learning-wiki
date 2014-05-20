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

##### - <a name="getSiblings"></a>getSiblings(boolean)

Returns a collection of all the current models siblings.

````
var mySiblings = Adapt.blocks[0].getSiblings();
// returns siblings if I'm a block but not return self.
````

````
var mySiblings = Adapt.blocks[0].getSiblings(true);
// returns my siblings if I'm a block and return self
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

##### - <a name="lockedAttributes"></a>set & Locked Attributes

We've taken Backbone's set and validate methods and added some extra functionality that enables Locked Attributes.

Now any model extending off Backbone.Model gets the ability to lock attributes and stop them from being changed without consent from other plugins that have changed that attribute.

Let's take the attribute ``_isVisible`` on a component. By default this is set to ``true``. If a plugin would like to change this then they need to pass in the plugin name in the options object:

```
componentModel.set('_isVisible', false, {pluginName:"_trickle"});
```

If no pluginName is added then this attribute will not be changed.

Locked Attributes works like a mediator between plugins and allows attributes to change if all plugins agree. Let's add to the situation above - Currently because only one plugin has changed it the attribute will change to ``false``. Another plugin then sets the same component ``_isVisible`` attribute to ``false``. 

```
// Can be written this way too
componentModel.set({'_isVisible':false}, {pluginName:"_triggered"});
```

The attribute stays as ``false``. However if one of the plugins decides to try and show the component:

```
componentModel.set('_isVisible', true, {pluginName:"_trickle"});
```

The model will not change to ``true`` as there is still one plugin set to ``false``.

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

##### - <a name="adapt-view-render"></a>render()

This method renders the view into the dom.

##### - <a name="adapt-view-preRender"></a>preRender()

This is a blank method that is used to setup components before they render.

##### - <a name="adapt-view-postRender"></a>postRender()

This is a blank method that is used in other views to setup anything on the view or model after rendering.

### Adapt

The main Adapt object can be used to pass events, grab the core collections of models or register a component. Adapt also has the following:

##### - Adapt.initialize

This is only able to be called once and fires off when all the content is loaded and Adapt is ready to begin. It triggers off a 'adapt:initialize' event and then starts the router.

##### - Adapt.course

This gives access to the course model that contains the course completion status, title and body. You can use all the AdaptModel methods:

[getChildren()](#getChildren)

[getParent()](#getParent)

[getSiblings()](#getSiblings)

[findAncestor(ancestors)](#findAncestor)

[findDescendants(descendants)](#findDescendants)

[setOnChildren(key, value, [options])](#setOnChildren)

##### - Adapt.contentObjects

This collection holds all the contentObjects including the pages.

##### - Adapt.articles

This collection holds all the article models.

##### - Adapt.blocks

This collection holds all the block models.

##### - Adapt.components

This collection holds all the component models.

##### Adapt.register

This is used to register components into the componentStore:

````
var HelloWorld = ComponentView.extend({
        
    postRender: function() {
        console.log('Hello to the world');
    }
    
});

Adapt.register("helloWorld", HelloWorld);

// Registers a "helloWorld" plugin into the componentStore
````

##### Adapt.componentStore

Used by BlockView when creating components. The BlockView is able to search the right component, by searching it's children and rendering the right component.

##### Adapt.drawer

Used to access the Drawer module. Please see [here](https://github.com/adaptlearning/adapt_framework/wiki/Core-modules#drawer) for more details.

##### Adapt.device

Returns an object with the following key/values:

* ``Adapt.device.browser`` - returns the users browser ``Chrome``.
* ``Adapt.device.version`` - returns the users browser version ``31``.
* ``Adapt.device.OS`` - returns the users operating system ``OS``.
* ``Adapt.device.screenSize`` - returns the current screen size and is updated when the window size changes. Can be one of the following: ``large``, ``medium`` or ``small``.
* ``Adapt.device.screenWidth`` - returns the current screen width and is updated when the window width changes. ``1024``.
* ``Adapt.device.touch`` - returns ``true`` or ``false`` based upon if the device is touch enabled.

This object is setup in device.js.

##### Adapt.currentLocation

This is set by the router and tracks the current location of the user. This can be two of the following:

* "course" - This is set when the router goes to the first route.
* ":id" - This "id" is set based upon what attribute is passed into the router.

If a plugin wanted to find out what the current page model is the can do the following:

````
if (Adapt.currentLocation !== "course") {
    var currentPageModel = Adapt.contentObjects.findWhere({
        "_id": Adapt.currentLocation
    });
}
````

##### Adapt.scrollTo

Used to wrap the ScrollTo plugin to enable events on start and end of the scroll.

```
// Syntax: Adapt.scrollTo(element, options);
Adapt.scrollTo('.a-05', {
    onAfter: function() {
        console.log('trigger this after page has scrolled');
    }
})
```

For more information on the options object please see [here](https://github.com/flesler/jquery.scrollTo)

By wrapping your page and menu scrollTo methods with Adapt.scrollTo() you get the benefit of these events:

* ``'page:scrollTo'`` - Triggered before the scroll when on a page - passes out the element.
* ``'menu:scrollTo'`` - Triggered before the scroll when on a menu - passes out the element.
* ``'page:scrolledTo'`` - Triggered after the scroll when on a page and the scroll has ended - passes out the element.
* ``'menu:scrolledTo'`` - Triggered after the scroll when on a menu and the scroll has ended - passes out the element.

##### Adapt.navigateToElement

This allows you to navigate to any core element within a page (article, block or component).

```
// Syntax: Adapt.navigateToElement(element, type, options);
Adapt.navigateToElement('.b-22', 'blocks', {duration: 3000});
```

This will navigate to a block with the ``_id`` 'b-22' - even if it's on another page. It's wrapped around ``Adapt.scrollTo`` so you get the benefit of the events being triggered.

For more information on the options object please see [here](https://github.com/flesler/jquery.scrollTo).

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