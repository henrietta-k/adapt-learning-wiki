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