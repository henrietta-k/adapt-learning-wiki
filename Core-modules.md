#####Quick links

[App](#app)

[NavigationView](#navigationView)

[Router](#router)

[Device](#device)

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

* Triggers an event 'router:handleId'
* Remove all currently active views.
* Show a loading status
* Set Adapt.currentLocation to the current "_id" being passed in.
* Search through the contentObjects collection and find the model with that "_id" and render either a menu or a page.
* Add a class to the "#wrapper" element based upon location, either 'location-content' or 'location-menu'.

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

The mediator is an events based module that enables developers to 'tap' in to Adapt's core functionality and prevent the default behaviour. It is important for extensions to be able to delay a core function being called, like displaying feedback to a user.

The core open ended events are attached through the ``Adapt.mediator.default`` method:

````
Adapt.mediator.default('questionView:feedback', function() {
    // This callback will be called if no ``event.preventDefault()`` is called
})
````