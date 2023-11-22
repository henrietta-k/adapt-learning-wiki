# Navigation

The following covers Core navigation functionality: [sorting order](https://github.com/adaptlearning/adapt_framework/wiki/Navigation/_edit#navigation-sorting-order), [button API](https://github.com/adaptlearning/adapt_framework/wiki/Navigation/_edit#navigation-button-api) and [tooltip API](https://github.com/adaptlearning/adapt_framework/wiki/Navigation/_edit#navigation-tooltip-api).

## Navigation sorting order 

The sorting order was introduced to give flexibility in the visual display of the navigation bar as well as accessibility compliance with [WCAG 2.0 Making the DOM order match the visual order](https://www.w3.org/TR/WCAG20-TECHS/C27.html).
The sorting of buttons is according to a `data-order` attribute in the DOM which is configured by `_navOrder` in _course.json_ `_globals._extensions`.

Sorting order is typically defined by a range from 0 (far left for LTR) to 100 (far right for RTL). Items positioned between 0 to 100 are usually in increments of 10.

`_spacers` can be used to create space between nav items. The default separates out the left and right aligned items. Multiple spacers can be used depending on the desired layout e.g. two spacers would give you left, centered and right aligned items.


## Navigation button API

The navigation button API was created to allow extensions to define buttons and add them to the navigation bar rather than allowing DOM injection.

* Backward compatible with injection
* Text label based upon the button aria label
* Ordering
* Icons
* Show/hide text


## Navigation tooltip API