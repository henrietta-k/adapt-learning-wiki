As of framework version 2.0.9, Adapt employs '_isLocked' as a [core model attribute](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes). Its default value is `false`. It is supported by the '_lockType' attribute and the 'checkLocking' function. The code governing these is found in [src/core/js/models/adaptModel.js](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/models/adaptModel.js).  

'_isLocked' is available on all models that extend Adapt.model. It is commonly used by menus to lock an item until a particular condition is satisfied, such as the completion of the previous item. Examples below focus on its use by menus.

### To lock an item
- Set `"_isLocked" = false`
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
        background-image: url('course/en/images/menu-item-locked.png.png');
        background-repeat: no-repeat;
    }
}
```  


## The Scenario  
A course presents a number of menu items to the learner. Of this number, only the first is enabled. After the learner completes the first, the other menu items (or some subset) are enabled and the learner now has access to them.

## How To 

1. Ensure your Adapt framework version is ^2.0.9
2. Ensure the menu includes [code snippet](https://github.com/adaptlearning/adapt-contrib-boxmenu/blob/master/js/adapt-contrib-boxmenu.js#L37), but implement the menu json normally per the *example.json* or README.
3. Add your "_lockType" to *course.json*
4. Style CSS and/or adjust JavaScript based on class locked.

## Lock Types
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
`,"_lockedBy": "co-XX"`
where `"co-XX"` is the Id of the object whose completion will enable this page or menu.

**effect**  
The all menu items are enabled except any item whose json contains the `"_lockedBy"` attribute. That item will be enabled only when the menu item specified by the value of `"_lockedBy"` is completed. 

CSS
_isComplete
_force

define completion
define enabled

*src/core/js/models/adaptModel.js*
Matt: please note that I have instructed that all lockTypes including custom to be assigned in course.json, and that custom requires an additional assignment of `_lockedBy`in contentObjects.json.

Complete page: Developers Guide: Menu. How to ensure the menu can be locked. 