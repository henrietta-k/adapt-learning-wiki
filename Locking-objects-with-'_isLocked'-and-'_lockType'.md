As of framework version 2.0.9, Adapt employs `_isLocked` as a [core model attribute](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes). Its default value is `false`. It is supported by the `_lockType` attribute and the `checkLocking` function. The code governing these is found in [src/core/js/models/adaptModel.js](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/models/adaptModel.js).  

`_isLocked` is available on all models that extend `Adapt.model`. It is commonly used by menus to lock an item until a particular condition is satisfied, such as the completion of the previous item. 

Examples below focus on its use by menus.

## To lock an item
Set `"_isLocked": true` in the object's model JSON, or set this model attribute within the plug-in's javascript code. Once set, the attribute can be referenced to determine behavior.  

## Using `"_isLocked"` to determine behavior 
Implement code in your JS, template, and CSS that checks the attribute and responds accordingly.  

JS example:  
```javascript  
className: function() {
    var nthChild = this.model.get("_nthChild");
    return [
        'menu-item',
        'menu-item-' + this.model.get('_id') ,
        this.model.get('_classes'),
        this.model.get('_isVisited') ? 'visited' : '',
        this.model.get('_isComplete') ? 'completed' : '',
        this.model.get('_isLocked') ? 'locked' : '',
        'nth-child-' + nthChild,
        nthChild % 2 === 0 ? 'nth-child-even' : 'nth-child-odd'
    ].join(' ');
},
```  
JS example:  
```javascript  
onClickMenuItemButton: function(event) {
    if(event && event.preventDefault) event.preventDefault();
    if(this.model.get('_isLocked')) return;
    Backbone.history.navigate('#/id/' + this.model.get('_id'), {trigger: true});
}
```  
Template example:  
```handlebars    
<div class="menu-item-inner {{#if _locked}}locked{{/if}}" aria-label="{{_globals._menu._mymenu.menuItem}}" {{#if _globals._menu._mymenu.menuItem}}tabindex="0"{{/if}}>

```  
CSS/Less example:  
```less  
.menu-item-inner {
    background-image: url('course/en/images/menu-item.png');
    background-repeat: no-repeat;
    &.locked {
        background-image: url('course/en/images/menu-item-locked.png');
        background-repeat: no-repeat;
    }
}
```  

## Using locking with menus  

Locking is frequently used with menus to control the learner's ability to access content. Adapt provides four types of locking: sequential, unlockFirst, lockLast, and custom. A locking type can be specified in the model json. For locking pages on a menu, this means that the course author adds `"_lockType": "sequential"` (or other lock type) to the menu itself.

> Note: Locking a menu or page directly using `"_isLocked": true` in JSON is incompatible with the use of `"_lockType"`. Do not mix the two techniques.

The normal use case has the menu at the root level of the course and so the `_lockType` should be added to *course.json*. For a sub-menu, the `_lockType` should be added to the content object (in *contentObjects.json*) which is the parent of the pages to be locked.
Example:  
```javascript  
"_id": "course",
"_type": "course",
"_lockType": "sequential", 
"title": "Adapt demonstration",
"displayTitle": "Adapt demonstration",
"description": "A sample course demonstrating the capabilities of the Adapt",
"body": "Welcome to the demonstration build of the Adapt framework.",
```

### sequential
**json**  
On the menu add the following:  
`,"_lockType": "sequential"`

**effect**  
The first menu item will be enabled. The following items will be disabled. Each item will be enabled when the preceding item is completed.

### unlockFirst
**json**  
On the menu add the following:  
`,"_lockType": "unlockFirst"`

**effect**  
The first menu item will be enabled. The following items will be disabled. When the first item is completed, all subsequent items will be enabled.

### lockLast
**json**  
On the menu add the following:  
`,"_lockType": "lockLast"`

**effect**  
The all menu items are enabled except the last item. The last item is enabled only when all other menu items have been completed.   

### custom
**json**  
On the menu add the following:  
`,"_lockType": "custom"`  
In *contentsObjects.json* add the following to the page or menu that you want locked:  
`,"_lockedBy": ["co-10", "co-15"]`  
where the value of `"_lockedBy"` is an array of one or more Ids of the object/s whose completion will enable this page or menu.

**effect**  
All menu items are enabled *except* any item whose json contains the `"_lockedBy"` attribute. That item will be enabled only when the menu item specified by the value of `"_lockedBy"` is completed. 

### `_forceRouteLocking`
Whilst the locking system in Adapt prevents the user from navigating to locked objects using the interface elements in the course, it does not prevent navigating to a locked object by changing the ID in the address bar. To prevent this, add the following to *config.json*:  
`,"_forceRouteLocking": true`

>Note: Many learning management systems launch the course in a browser window where the address bar cannot be accessed by the user, so this is generally not an issue. In addition, having the ability to bypass the locking during course development and testing can be useful.  

## Document for your users  
When using locking with a plug-in, remember to document its use in your README and to provide sample configuration in *example.json*.  