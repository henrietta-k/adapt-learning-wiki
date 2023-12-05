# Navigation

The following covers Core navigation functionality: [sorting order](https://github.com/adaptlearning/adapt_framework/wiki/Navigation/_edit#navigation-sorting-order), [button API](https://github.com/adaptlearning/adapt_framework/wiki/Navigation/_edit#navigation-button-api) and [tooltip API](https://github.com/adaptlearning/adapt_framework/wiki/Navigation/_edit#navigation-tooltip-api).

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

## Navigation button API

The navigation button API was created to allow extensions to define buttons and add them to the navigation bar rather than allowing DOM injection.

* Backward compatible with injection
* Text label based upon the button aria label
* Ordering
* Icons
* Show/hide text



## Navigation tooltip API
JSON in _course.json_ to enable / disable globally:<br>
```
"_tooltips": {
  "_isEnabled": true
}
```