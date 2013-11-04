### Events

To tap into our internal event system you would need to require 'coreJS/adapt' and use the following methods.

trigger - triggers a global event

on - listens to a global event and calls a callback

off - removes the global event attached to an object

    define(['coreJS/adapt'], function(Adapt) {
        
        Adapt.on('pluginName:changed', function() {

        });

        Adapt.trigger('pluginName:changed');

    })