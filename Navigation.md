# Navigation

The following covers Core navigation functionality: [sorting order](https://github.com/adaptlearning/adapt_framework/wiki/Navigation#navigation-sorting-order), [button API](https://github.com/adaptlearning/adapt_framework/wiki/Navigation#navigation-button-api) and [tooltip API](https://github.com/adaptlearning/adapt_framework/wiki/Navigation#navigation-tooltip-api).

## Navigation sorting order 

The sorting order was introduced to give flexibility in the visual display of the navigation bar as well as accessibility compliance with [WCAG 2.0 Making the DOM order match the visual order](https://www.w3.org/TR/WCAG20-TECHS/C27.html).
The sorting of buttons is according to a `data-order` attribute in the DOM which is configured by `_navOrder` in _course.json_ `_globals._extensions`.

Core navigation:
<pre>
    "_extensions": {
      "_drawer": {
        "_navOrder": 100
      },
      "_navigation": {
        "_skipButton": {
          "_navOrder": -100
        },
        "_backButton": {
          "_navOrder": 0
        },
        "_spacers": [
          {
            "_navOrder": 0
          }
        ]
      }
    }
</pre>

Navigation plugins also support `_navOrder`, for example [pageLevelProgress](https://github.com/adaptlearning/adapt-contrib-pageLevelProgress/blob/a82f33a7de45517d4537552fde451ef8e31011ff/example.json#L5) or [Visua11y](https://github.com/cgkineo/adapt-visua11y/blob/86ed44686719b0284b5cac141966d7f586f08be4/example.json#L4).

Sorting order is typically defined by a range from 0 (far left for LTR) to 100 (far right for LTR). Items positioned between 0 to 100 are usually in increments of 10.

`_spacers` can be used to create space between nav items. The default separates out the left and right aligned items. Multiple spacers can be used depending on the desired layout e.g. two spacers would give you left, centered and right aligned items (see below).

Visual navigation display:<br><br>
<img width="867" alt="navOrder_example" src="https://github.com/adaptlearning/adapt_framework/assets/7045330/9c300bca-5c17-4dea-979a-e98a553cffc0"><br><br>
DOM order:<br><br>
<img width="586" alt="navOrder_dom" src="https://github.com/adaptlearning/adapt_framework/assets/7045330/497e7836-0912-4396-b06c-b3f08d0b0824"><br><br>
JSON in _course.json_ `_globals`:<br>
<pre>
    "_extensions": {
      "_drawer": {
        "_navOrder": 100
      },
      "_navigation": {
        "_skipButton": {
          "_navOrder": -100
        },
        "_backButton": {
          "_navOrder": 0
        },
        "_spacers": [
          {
            "_navOrder": 20
          },
          {
            "_navOrder": 80
          }
        ]
      },
      "_navigationTitle": {
        "_navOrder": "30"
      },
      "_close": {
        "_navOrder": "150"
      }
    }
</pre>



***

## Navigation button API

The navigation button API was created to allow extensions to define buttons and add them to the navigation bar rather than allowing DOM injection. API features include:

* Supports backward compatibility with injection
* Display button text label based upon the button aria label
* Display button icons
* Ordering
* Show/hide text


Core navigation:<br>
JSON in _course.json_ to globally configure navigation button text labels:
```
"_navigation": {
  "_showLabel": true, // Show navigation button labels
  "_showLabelAtWidth": "medium", // Show label at this breakpoint and higher
  "_labelPosition": "auto" // Where to show the label in relation to the button icons 
}
```
When the user's browser window is at least the size specified in `_showLabelAtWidth` or greater, the text labels will be shown. Options include `any`, `small`, `medium` and `large`. `small`, `medium` and `large` refer to the standard Adapt breakpoints (see default [screenSize](https://github.com/adaptlearning/adapt-contrib-core/blob/852ef1269dcdfc220361d500c473c9042ffa65f4/schema/config.model.schema#L191) values). The `any` option will show the label at any size.

The `_labelPosition` refers to where to show the label in relation to the button icons. Options inlclude `auto`, `top`, `bottom`, `left` and `right`.<br> 
`auto` - default display, inherits from lang direction [ icon / text] for LTR and [ text / icon ] for RTL<br>
`left` - label displays left of icon regardless of lang direction [ text / icon ]<br>
`right` - label displays right of icon regardless of lang direction [ icon / text]

Navigation plugins also support `navLabel`, for example [pageLevelProgress](https://github.com/adaptlearning/adapt-contrib-pageLevelProgress/blob/a82f33a7de45517d4537552fde451ef8e31011ff/example.json#L6C12-L6C20) or [Visua11y](https://github.com/cgkineo/adapt-visua11y/blob/0eae8306eb0f4479fa8d3595e5b931f7077cc650/example.json#L5).

### Navigation model
* `NavigationButtonModel` To hold the properties for each button
* `NavigationButtonView` For extensions to make their own buttons and for legacy injected button management
* `NavigationModel` To hold the navigation configuration
* All model updates will be reflected in the DOM.

### General API layout
```js
import navigation from 'core/js/navigation';
navigation.model.set('_showLabel', true); // Show all labels

const backButton = navigation.getButton('back');
backButton.set('_order', 400); // Move the back button to the right
backButton.set('text', 'New Label'); // Change the back button label text


navigation.removeButton(backButton); // Remove back button

// Remove all buttons
navigation.buttons.forEach(button => navigation.removeButton(button));
```

Example, making a home button:

![image](https://user-images.githubusercontent.com/7974663/228893292-c4737ad4-a768-437e-9075-ca3f5481fcc8.png)


```js
import Adapt from 'core/js/adapt';
import navigation from 'core/js/navigation';
import NavigationButtonModel from 'core/js/models/NavigationButtonModel';
import NavigationButtonView from 'core/js/views/NavigationButtonView';

// Extend the model and view classes to add own behaviour

Adapt.on('navigation:ready', () => {
  const model = new NavigationButtonModel({
    _id: 'home',
    _order: 0,
    _event: 'homeButton',
    _showLabel: null,
    _classes: '',
    _iconClasses: 'icon-medal',
    _role: 'link',
    ariaLabel: 'Home',
    text: '{{ariaLabel}}'
  });
  const view = new NavigationButtonView({ model });
  navigation.addButton(view);
});
```

Each button has the potential for custom `_id`, `_order`, `_event`, `_showLabel`, `_classes`, `_iconClasses`, `_role`, `ariaLabel` and `text`, with global settings for `_showLabel`, `_navigationAlignment` and `_isBottomOnTouchDevices`.

`_event` has some default behaviour at `"backButton"`, `"homeButton"`, `"parentButton"`, `"skipNavigation"` and `"returnToStart"`.



Example, added visua11y and the above home button to the vanilla course:

![image](https://user-images.githubusercontent.com/7974663/228896348-be925656-bbe8-40d2-bf35-a3b046f83895.png)


### Backward compatibility
Older buttons should have an `aria-label` attribute or an `.aria-label` element in order for a text label to be automatically generated. A `<span class="label" aria-hidden="true">{{ariaLabel}}</span>` will be appended automatically to any existing button, if it doesn't exist, and will otherwise be automatically updated from the value of the `aria-label` attribute or `.aria-label` element. This is as model `text` defaults to `{{ariaLabel}}`. On older buttons `"ariaLabel"`, `"_role"` and `"_classes"` have no effect when changed from the model as they should be supplied by the injected buttons themselves. `"text"`, `"_order"`, `"_showLabel"`, `"_id"` and `"_event"` should work as expected on older injected buttons.


***

## Navigation tooltip API

Tooltips display on mouseover and focus. Tooltips are read by a screenreader on mouseover, on focus the screen reader will read the target's aria label. The button `aria-label` is used to set the default tooltip `text`.  

JSON in _course.json_ to enable / disable globally:<br>
```
"_tooltips": {
  "_isEnabled": true
}
```
Core navigation:<br>
JSON in _course.json_ `_globals._extensions` to configure Back button and Drawer button:
```
"_extensions": {
  "_navigation": {
    "_backNavTooltip": {
      "_isEnabled": true,
      "text": "{{ariaLabel}}"
    }
  },
  "_drawer": {
    "_navTooltip": {
      "_isEnabled": true,
      "text": "{{ariaLabel}}"
    }
  }
}
```
Navigation plugins also support `_navTooltip`, for example [pageLevelProgress](https://github.com/adaptlearning/adapt-contrib-pageLevelProgress/blob/a82f33a7de45517d4537552fde451ef8e31011ff/example.json#L9C12-L9C23) or [Visua11y](https://github.com/cgkineo/adapt-visua11y/blob/0eae8306eb0f4479fa8d3595e5b931f7077cc650/example.json#L6).