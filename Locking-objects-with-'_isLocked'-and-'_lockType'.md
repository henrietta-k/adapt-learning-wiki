As of framework version 2.0.9, Adapt employs '_isLocked' as a [core model attribute](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes). Its default value is `false`. It is supported by the '_lockType' attribute and the 'checkLocking' function. The code governing these is found in [src/core/js/models/adaptModel.js](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/models/adaptModel.js).  

'_isLocked' is available on all models that extend Adapt.model. It is commonly used by menus to lock an item until a particular condition is satisfied, such as the completion of the previous item. Examples below focus on its use by menus.

## To lock an item
- Set `"_isLocked" = false`  
    - This is typically accomplished by setting a `"_lockType"` on the object's json and is typically done by the course author. A developer may, of course, accomplish this differently within the plug-in's code.
- Implement code in your JS, template, and CSS that checks the attribute and responds accordingly.  

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

## Configure type of locking  

Adapt provides four types of locking: sequential, unlockFirst, lockLast, and custom. Which is used is determined by the model json. For menus, this means that the course author adds `"_lockType": "sequential"` (or other lock type) to the menu object or page object in *course.json*.

### sequential
**json**  
In *course.json* add the following:  
`,"_lockType": "sequential"`

**effect**  
The first menu item will be enabled. The following items will be disabled. Each item will be enabled when the preceding item is completed.

### unlockFirst
**json**  
In *course.json* add the following:  
`,"_lockType": "unlockFirst"`

**effect**  
The first menu item will be enabled. The following items will be disabled. When the first item is completed, all subsequent items will be enabled.

### lockLast
**json**  
In *course.json* add the following:  
`,"_lockType": "lockLast"`

**effect**  
The all menu items are enabled except the last item. The last item is enabled only when all other menu items have been completed.   

### custom
**json**  
In *course.json* add the following:  
`,"_lockType": "custom"`  
In *contentsObjects.json* add the following to the page or menu that you want locked:  
`,"_lockedBy": ["co-XX"]`
where `"co-XX"` is a comma-separated list of the Id/s of the object/s whose completion will enable this page or menu.

**effect**  
All menu items are enabled *except* any item whose json contains the `"_lockedBy"` attribute. That item will be enabled only when the menu item specified by the value of `"_lockedBy"` is completed. 

### `_forceRouteLocking`
Using `_isLocked` and `_lockType` affects the learner's interaction with on-screen elements. It does not lock down the ability to navigate to pages using the browser's address bar. If this is a concern, the course author  can prevent this by adding the following in *config.json*:
`,"_forceRouteLocking": true`

## Document for your users  
When using locking with a plug-in, remember to document its use in your README and to provide sample configuration in *example.json*.  