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

```html
<a href="#" data-event="backButton"><span>Back button</span></a>
```

The Navigation View will then trigger an event based up the elements data-event:

```js
Adapt.trigger('navigation:backButton');
```

### <a name="router"></a>Router

When initialized, the router sets up the course title as the HTML document title. Adapt has a simple routing system with only three routes. The first route handles loading the course object, the second route handles an `_id` attribute being passed in and the third handles routes for plugins. 

When an `_id` attribute is passed in:

```
"#/id/co-05"
```

the router will follow this order:

* Remove all currently active views.
* Show a loading status.
* Set contentObjects to visited.
* Set Adapt.location object to the current `_id` being passed in. Add a class to the `#wrapper` element based upon location.
* Search through the contentObjects collection and find the model with that `_id`. Then render either a menu or a page.

The `navigateToPreviousRoute` method mimics the back button of the browser whilst keeping the user within an Adapt course. This is the default way Adapt routes but can be overwritten like this:

```js
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

```js
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

```js
Adapt.on('device:resize', function(windowWidth) {
    console.log("Any time the window resizes I will be called and here's the new window width: ", windowWidth);
});
```

* ``'device:changed'`` - This is fired when the screen size changes between the set screen sizes ('large', 'medium', 'small') and passes the new screen size as an argument.

```js
Adapt.on('device:changed', function(deviceSize) {
    console.log("Any time the device size changes I will be called and here's the new device size: ", deviceSize);
});
```

### <a name="drawer"></a>Drawer

The Drawer module is a slide out panel from the right hand side. Drawer has two main features:

* Item view - Enables plugins to add to the Drawer list. Each item can have a title, body and custom css class attached to the Drawer item. When a Drawer item is clicked it triggers a callback event.
* Custom view - Enables plugins to add a custom view into the Drawer pull out. This is then managed via the plugin itself.

To add an item to the Drawer you need to listen to the ``'app:dataReady'`` event and add your item:
```js
// Listen to 'app:dataReady'
Adapt.on('app:dataReady', function() {
    var drawerObject = {
        title: "Title of my Drawer item",
        description: "A nice little description of my drawer item and possibly what I expect to see when clicked on.",
        className: 'custom-class-added-to-item'
    };
    Adapt.drawer.addItem(drawerObject, 'pageLevelProgress:show');
});
```

To add a custom view into the Drawer pull out use the following (remember that this invokes the view straight away):

```js
Adapt.drawer.triggerCustomView(new PageLevelProgressView({collection:this.collection}).$el, false);
```

Custom views should deal with their own removing and closing of Drawer. To close the Drawer pull out, use `'drawer:closeDrawer'`. Custom views also have the ability to show a back button. This is set to show by default. The back button takes the user back to the Drawer item view

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
```js
var popupObject = {
    title: "Popup title",
    body: "This is a popup to add additional information - please close me by pressing the 'x'"
};

Adapt.trigger('notify:popup', popupObject);// if using Adapt FW v4.3.0 or earlier

Adapt.notify.popup(popupObject);// if using Adapt FW v4.4.0 or later (the above will still work but will be removed in a future release)
```

The popupObject has an `_isCancellable` property. If set to `false`:
* the popup can only be closed via the `notify:close` event.
* the cancel button will be removed. 
* clicking on the shadow will not close the popup
* triggering the `notify:cancel` event will not close the popup. 

`_isCancellable` defaults to `true`

The popup can also be appended with a sub view via the `_view` property.

```js
var popupObject = {
    "title": "this is a text",
    "_isCancellable": false,
    _view: new PopupView({ model: new Backbone.Model({}) })
};
```
This sub view can be fully configured:

```js
var PopupView = Backbone.View.extend({

  events: {
    "click button.cancel": "onCancelClick",
    "click button.close": "onCloseClick"
  },

  onCancelClick: function() {
    console.log("SUBNOTIFY: button.cancel clicked");
    Adapt.trigger("notify:cancel");
  },

  onCloseClick: function() {
    console.log("SUBNOTIFY: button.close clicked");
    Adapt.trigger("notify:close");
  },

  initialize: function() {
    console.log("SUBNOTIFY: initialized");
    this.listenToOnce(Adapt, {
      "notify:opened": this.onOpened,
      "notify:closed": this.onClosed,
      "notify:cancelled": this.onCancelled
    });
    this.render();
  },

  render: function() {
    this.$el.append("this is a sub view <button class='cancel'>click here to cancel</button><button class='close'>click here to close</button>");
  },

  onOpened: function(notifyView) {
    // notifyView.subView === this
    if (notifyView.subView.cid !== this.cid) return;
    console.log("SUBNOTIFY: opened");
  },

  onClosed: function() {
    // called when notify is closed
    console.log("SUBNOTIFY: closed");
  },

  onCancelled: function() {
    // called when notify is cancelled
    console.log("SUBNOTIFY: cancelled");
  },

  remove: function() {
    // called when notify is closed
    console.log("SUBNOTIFY: removed");
    Backbone.View.prototype.remove.apply(this, arguments);
  }

});
```

How to activate an alert:

```js
var alertObject = {
    title: "Alert",
    body: "Oops - looks like you've not passed this assessment. Please try again.",
    confirmText: "Ok",
    _isCancellable: false,
    _callbackEvent: "assessment:notPassedAlert",
    _showIcon: true
};

Adapt.trigger('notify:alert', alertObject);// if using Adapt FW v4.3.0 or earlier

Adapt.notify.alert(alertObject);// if using Adapt FW v4.4.0 or later (the above will still work but will be removed in a future release)
```
The alertObject has two specific properties. `confirmText` allows you to change the text of the confirm button presented in the alert popup. This button will dismiss the popup even if `_isCancellable: false` is set.

`_callbackEvent` allows you to specify an event that will be triggered when the confirmText button is clicked. In the above example, we would want our code to be listening for the `assessment:notPassedAlert` event.
```js
Adapt.on('assessment:notPassedAlert', function() {
    //do something
})
```

How to activate a prompt dialogue:
```js
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

Adapt.trigger('notify:prompt', promptObject);// if using Adapt FW v4.3.0 or earlier

Adapt.notify.alert(promptObject);// if using Adapt FW v4.4.0 or later (the above will still work but will be removed in a future release)
```

How to activate a push notification:
```js
var pushObject = {
    title: "Great work!",
    body: "You've just done something that merited a push notification.",
    _timeout: 5000,
    _callbackEvent: "pushNotify:clicked" // The _callbackEvent is triggered only if the push notification is clicked
};

Adapt.on('pushNotify:clicked', function() {
    console.log('A push notification was clicked');
});

Adapt.trigger('notify:push', pushObject);// if using Adapt FW v4.3.0 or earlier

Adapt.notify.push(pushObject);// if using Adapt FW v4.4.0 or later (the above will still work but will be removed in a future release)
```

#### Notify Events

Note: the alert/prompt/popup/push events are deprecated as of Adapt v4.4.0 - they will still work but will be removed in a future release. Please update to using the new Notify API.

Event | Argument | Description
--- | --- | ---
`notify:popup` | `popupObject = {title: "Popup Title", body: "Body"}` | Triggers a popup
`notify:prompt` | `promptObject = {_prompts: [{promptText: "Yes", _callbackEvent: "event"}]}` | Triggers a prompt popup
`notify:alert` | `alertObject = {confirmText: "OK", _callbackEvent: "event"}` | Triggers an alert popup
`notify:push` | `pushObject = {_timeout: 5000, _callbackEvent: "pushNotify:clicked"}` | Triggers a push popup
`notify:pushShown` | | Triggers when a push popup is displayed
`notify:pushRemoved` | | Triggers when a push popup is clicked by the user
`notify:opened` | | Triggered when popup is opened
`notify:close` | | Triggered by close button. Will work even when `_isCancellable:false` is set
`notify:closed` | | Triggers when `closeNotify()` is run
`notify:cancel` | | Triggered by cancel button or clicking on popup shadow. Disabled by setting `_isCancellable:false`
`notify:cancelled` | | Triggers when `cancelNotify()` is run

#### Notify API
The Notify API was added in Adapt v4.4.0 - it can be accessed at `Adapt.notify` and has the following public methods:
* `alert`
* `prompt`
* `popup`
* `push`

All of which accept an object containing the notify settings as the only parameter.

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