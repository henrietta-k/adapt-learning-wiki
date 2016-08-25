##### Quick links

* [App](#app)
* [NavigationView](#navigationView)
* [Router](#router)
* [Device](#device)
* [Drawer](#drawer)
* [Notify](#notify)
* [Popup Manager](#popupManager)
* [Helpers](#helpers)

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

When initialized, the router sets up the course title as the HTML document title. Adapt has a simple routing system with only three routes. The first route handles loading the course object, the second route handles an "_id" attribute being passed in and the third handles routes for plugins. 

When an "_id" attribute is passed in:

````
"#/id/co-05"
````

the router will follow this order:

* Remove all currently active views.
* Show a loading status.
* Set contentObjects to visited.
* Set Adapt.location object to the current "_id" being passed in. Add a class to the "#wrapper" element based upon location.
* Search through the contentObjects collection and find the model with that "_id". Then render either a menu or a page.

The ``navigateToPreviousRoute`` method mimics the back button of the browser whilst keeping the user within an Adapt course. This is the default way Adapt routes but can be overwritten like this:

```
// Using locked attributes a plugin can change the default navigation
// Set _canNavigate to false
Adapt.router.set('_canNavigate', false, {pluginName: '_pageLevelProgress'});

// Listen to navigation event and add custom navigation
Adapt.on('navigation:backButton', function() {
    // Always navigate to the course menu
    Backbone.history.navigate('#', {trigger:true});
});
```

The router allows a three level routing system for plugins. When using the router to navigate through a plugin the following syntax is used:

``#/:pluginName(/*location)(/*action)``

``pluginName`` is needed whilst ``location`` and ``action`` are optional. When a user is navigated to a plugin route the router sets the Adapt.location object and triggers an event:

```
// If the plugin route was
// #/myPluginName/views/edit
// Then Adapt will trigger:
Adapt.trigger('router:plugin:myPluginName');
// Passing out the three levels of the route

// To listen to the plugin route
Adapt.on('router:plugin:myPluginName', function(pluginName, location, action) {
    console.log(pluginName, location, action);
    // Logs 'myPluginName', 'views', 'edit'
});
```

Plugins should not be adding classes to the #wrapper element as they get removed by the router - instead we suggest adding them to the HTML element.

### <a name="device"></a>Device

The device module detects which browser the user is on and adds the following classes to the ``<HTML>`` tag:

* Browser - ``Chrome``
* Version - ``version-32``
* OS - ``OS-Mac``

As well as adding these classes, device.js triggers some events: 

* ``'device:resize'`` - This should be used to find out when the browser has resized and passes the new window size as an argument.

````
Adapt.on('device:resize', function(windowWidth) {
    console.log("Any time the window resizes I will be called and here's the new window width: ", windowWidth);
});
````

* ``'device:changed'`` - This is fired when the screen size changes between the set screen sizes ('large', 'medium', 'small') and passes the new screen size as an argument.

````
Adapt.on('device:changed', function(deviceSize) {
    console.log("Any time the device size changes I will be called and here's the new device size: ", deviceSize);
});
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
// Adapt.drawer.triggerCustomView([$element], [showBackButton:boolean]);
Adapt.drawer.triggerCustomView(new PageLevelProgressView({collection:this.collection}).$el, false);
```

Custom views should deal with their own removing and closing of Drawer. To close the Drawer pull out, use ``'drawer:closeDrawer'``. Custom views also have the ability to show a back button. This is set to show by default. The back button takes the user back to the Drawer item view

Drawer passes out a few useful events:

``'drawer:opened'`` - When Drawer is opened.

``'drawer:closed'`` - When Drawer is closed.

``'drawer:openedItemView'`` - When Drawer is opening the standard Item View.

``'drawer:openedCustomView'`` - When Drawer is opening a Custom View.


### <a name="notify"></a>Notify

Adapt has an internal notifications system and can trigger four types of notifications:

* Popup - Used for when you need to popup some additional information. Similar to the feedback plugin Tutor.
* Alert - Used to get the users attention. Has a confirm button that needs clicking before progressing further in the course. The confirm button triggers a callback event.
* Prompt - Used for when the learner needs to make a choice. The prompts can have unlimited button options but we suggest three is the maximum. Each prompt button triggers a callback event.
* Push - Used to push an unobtrusive message to the learner. Similar to Mac OS growl. Only two push notifications are displayed at once whilst the others are push into a queue.

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

How to activate a push notification:
```
var pushObject = {
    title: "Great work!",
    body: "You've just done something that merited a push notification.",
    _timeout: 5000,
    _callbackEvent: "pushNotify:clicked" // The _callbackEvent is triggered only if the push notification is clicked
};

Adapt.on('pushNotify:clicked', function() {
    console.log('A push notification was clicked');
});

Adapt.trigger('notify:push', pushObject);
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