#####Quick links

[App](#app)

[NavigationView](#navigationView)

[Router](#router)

[Device](#device)

[Mediator](#mediator)

[Drawer](#drawer)

[Notify](#notify)

[Popup Manager](#popupManager)

[Helpers](#helpers)

### <a name="app"></a>App

This is where all the main loading and setup of Adapt begins. All the core Adapt Collections are instantiated and checked whether they have loaded their data.

### <a name="navigationView"></a>NavigationView

The NavigationView controls the top navigation bar. To keep a nice separation of plugins, any icon or button placed in this view should contain a 'data-event' attribute:

````
<a href="#" data-event="backButton"><span>Back button</span></a>
````

The Navigation View will then trigger an event based up the elements data-event:

````
Adapt.trigger('navigation:backButton');
````

### <a name="router"></a>Router

When initialized, the router sets up the course title as the HTML document title. Adapt has a simple routing system with only two routes. The first route handles loading a course whilst the second route handles an "_id" attribute being passed in. When an "_id" attribute is passed in:

````
"#/id/co-05"
````

the router will follow this order:

* Remove all currently active views.
* Show a loading status.
* Set contentObjects to visited.
* Set Adapt.currentLocation to the current "_id" being passed in. Add a class to the "#wrapper" element based upon location, either 'location-content' or 'location-menu'.
* Search through the contentObjects collection and find the model with that "_id" and render either a menu or a page.

The ``navigateToParent`` function finds the parent item of the current content object, and navigates to it. Using this function, 'upward' navigation of a course can be achieved - i.e. navigation between the current content and it's parent. The function is triggered by the ``navigation:menu`` event - currently, NavigationView triggers this event when the navigation menu icon is clicked.

When plugins use their own routers it's important to update the Adapt.currentLocation, class and attributes on the #wrapper. A plugin can do this by triggering this event:

```
// Syntax: Adapt.trigger('router:updateLocation', locationObject);
Adapt.trigger('router:updateLocation', {location:'my-plugin-name', id:'my-plugin-name-id'});
```

The ``locationObject`` above allows just the location key and value to be passed on. By doing this the ``id`` will be the same as the ``location`` value.

By setting this you are updating Adapt.currentLocation to the id, adding a class of location-[location] and a data attribute of data-location of the location. Plugins should not be adding classes to the #wrapper element.

### <a name="device"></a>Device

The device module detects which browser the user is on and adds the following classes to the ``<HTML>`` tag:

* Browser - ``Chrome``
* Version - ``version-32``
* OS - ``OS-Mac``

As well as adding these classes, device.js triggers an event ``'device:resize'``. This should be used to find out when the browser has resized and passes the new window size as an argument.

````
Adapt.on('device:resize', function(windowWidth) {
    console.log("Any time the window resizes I will be called and here's the new window width: ", windowWidth);
});
````

### <a name="mediator"></a>Mediator

The mediator is an events based module that enables developers to 'tap' in to Adapt's core functionality and prevent the default behaviour. It is important for extensions to be able to delay a core function being called, like displaying feedback to a user. Once a default callback has been created it can never be overwritten.

The core open ended events are attached through the ``Adapt.mediator.default`` method:

````
var feedback {
    title: "Yeah, you got this correct!",
    body: "It turns out that Adapt is Open Source and free to use."
}

Adapt.mediator.default('questionView:feedback', function(attributes) {
    // This callback will be called if no event.preventDefault() is called
    // The only argument passed in is from the original event arguments
    // attributes.title = "Yeah, you got this correct!"
});

Adapt.trigger('questionView:feedback', feedback);
````

To add a callback to the mediator use ``Adapt.mediator.on`` and pass the event name and callback. The callback is passed two arguments: 

* ``event`` - Use ``event.preventDefault();`` to prevent the default callback from happening.
* ``attributes`` - This is the original attributes passed into the event.

Any amount of callbacks can be attached to a default callback and all of the callbacks will be called before the default:

````
var feedback {
    title: "Yeah, you got this correct!",
    body: "It turns out that Adapt is Open Source and free to use."
}

Adapt.mediator.default('questionView:feedback', function(attributes) {
    // This callback will be called if no event.preventDefault() is called
    // The only argument passed in is from the original event arguments
    // attributes.title = "Yeah, you got this correct!"
});

Adapt.mediator.on('questionView:feedback', function(event, attributes) {
    event.preventDefault();
    // If event.preventDefault() is called then the callback above won't be called
    console.log(attributes.title); // "Yeah, you got this correct!"
})

Adapt.trigger('questionView:feedback', feedback);

// The default callback does not get called due to event.preventDefault() being called
````

### <a name="drawer"></a>Drawer

The Drawer module is a slide out panel from the right hand side. Drawer has two main features:

* Item view - Enables plugins to add to the Drawer list. Each item can have a title, body and custom css class attached to the Drawer item. When a Drawer item is clicked it triggers a callback event.
* Custom view - Enables plugins to add a custom view into the Drawer pull out. This is then managed via the plugin itself.

To add an item to the Drawer you need to listen to the ``'app:dataReady'`` event and add your item:
```
// Listen to 'app:dataReady'
Adapt.on('app:dataReady', function() {
    var drawerObject = {
        title: "Title of my Drawer item",
        description: "A nice little description of my drawer item and possibly what I expect to see when clicked on.",
        className: 'custom-class-added-to-item'
    };
    // Syntax for adding a Drawer item
    // Adapt.drawer.addItem([object], [callbackEvent]);
    Adapt.drawer.addItem(drawerObject, 'pageLevelProgress:show');
});
```

To add a custom view into the Drawer pull out use the following (remember that this invokes the view straight away):

```
// Syntax for adding a custom Drawer view
// Adapt.drawer.triggerCustomView([$element]);
Adapt.drawer.triggerCustomView(new PageLevelProgressView({collection:this.collection}).$el);
```

Custom views should deal with their own removing and closing of Drawer. To close the Drawer pull out, use ``'drawer:closeDrawer'``

Drawer passes out a few useful events:

``'drawer:opened'`` - When Drawer is opened.

``'drawer:closed'`` - When Drawer is closed.

``'drawer:openedItemView'`` - When Drawer is opening the standard Item View.

``'drawer:openedCustomView'`` - When Drawer is opening a Custom View.


### <a name="notify"></a>Notify

Adapt has an internal notifications system and can trigger three types of notifications:

* Popup - Used for when you need to popup some additional information. Similar to the feedback plugin Tutor.
* Alert - Used to get the users attention. Has a confirm button that needs clicking before progressing further in the course. The confirm button triggers a callback event.
* Prompt - Used for when the learner needs to make a choice. The prompts can have unlimited button options but we suggest three is the maximum. Each prompt button triggers a callback event.

How to activate a popup:
```
var popupObject = {
    title: "Popup title",
    body: "This is a popup to add additional information - please close me by pressing the 'x'"
};

Adapt.trigger('notify:popup', popupObject);
```

How to activate an alert:
```
var alertObject = {
    title: "Alert",
    body: "Oops - looks like you've not passed this assessment. Please try again.",
    confirmText: "Ok",
    _callbackEvent: "assessment:notPassedAlert",
    _showIcon: true
};

Adapt.trigger('notify:alert', alertObject);
```

How to activate a prompt dialogue:
```
var promptObject = {
    title: "Leaving so soon?",
    body: "Looks like you're trying to leave this page, yet you haven't completed all the learning. Would you like to stay on this page and complete it?",
    _prompts:[
        {
            promptText: "Yes",
            _callbackEvent: "pageLevelProgress:stayOnPage",
        },
        {
            promptText: "No",
            _callbackEvent: "pageLevelProgress:leavePage"
        }
    ],
    _showIcon: true
}

Adapt.trigger('notify:prompt', promptObject);
```

### <a name="popupManager"></a>Popup Manager

The popup manager should be triggered anytime you open or close a popup. Although this is a small module it is responsible for returning the users scroll position back to where the popup was triggered. This helps solve a problem where the user can scroll behind a popup and will loose their positioning on the page.

When triggering a popup to open please use ``Adapt.trigger('popup:opened');`` and when closing the popup use ``Adapt.trigger('popup:closed');``.

### <a name="helpers"></a>Helpers

We have a few helper functions for Handlebars. These can be used in your templates to help with attributes and adding extra logic.

* ``{{lowerCase title}}`` - returns the attribute 'title' in lowercase. Second attribute can be any string attribute from the model.
* ``{{numbers @index}}`` - returns a number listing when used within a ``{{#each}} {{/each}}`` iteration.
* ``{{capitalise title}}`` - returns the attribute 'title' with the first letter capitalised. Second attribute can be any string attribute from the model.
* ``{{odd @index}}`` - returns either 'even' or 'odd' when used within a ``{{#each}} {{/each}}`` iteration. Used when you need 'odd' or 'even' classes on items.
* ``{{#if_value_equals _type "component"}}[block of html]{{/if_value_equals}}`` - returns the [block of html] if the first argument is equal to the second.