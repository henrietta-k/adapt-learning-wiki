# _config.json_   

_config.json_ is located at [_/src/course/config.json_](https://github.com/adaptlearning/adapt_framework/blob/master/src/course/config.json). This required file is included with the installation of the Adapt framework and the Adapt authoring tool. 

>**Note**: What's the difference between _config.json_ and _course.json_?  
- _config.json_ contains settings that determine how your Adapt project **functions**. Whereas _course.json_ is focused on **content** that is used throughout your course, oftentimes being reused by various components and other plug-ins. 
-  _config.json_ resides **outside** of the language folder and _course.json_ resides **inside** (e.g., _/src/course/en_). Settings that are language dependent go in _course.json_.   
 
## Settings Overview

The properties listed below and their values are used to configure an Adapt project. Reference [_config.json_](https://github.com/adaptlearning/adapt_framework/blob/master/src/course/config.json) on GitHub to see them properly formatted as JSON. [_Configuration Settings_](https://github.com/adaptlearning/adapt_authoring/wiki/Configuration-settings) provides information about how they appear in the [authoring tool](https://github.com/adaptlearning/adapt_authoring/wiki).

### Attributes  

**_defaultLanguage** (string): This value represents the primary language in which course content will appear. A subfolder of _/course_ is created using this value (e.g., _/course/en_). Its value is assigned to the "lang" attribute of the HTML tag (e.g., &lt;html lang='en'&gt;). It is recommended to choose values from the [IANA language tag registry](http://www.iana.org/assignments/language-tags).  

**_defaultDirection** (string): This value is used to set the base direction of text for display. Adapt's default direction is left-to-right (`ltr`). To enable HTML for such right-to-left scripts as Arabic and Hebrew, use the value `rtl`. This will add the 'dir-rtl' class to the html tag. (No similar class is added for `ltr`.)  

**screenSize** (object): The **screen size** group allows pixel widths to be assigned to three device widths: **small**, **medium**, and **large**. Values assigned must be numbers only; include no measurement unit. Note: The screen sizes set the Adapt.device.width that is used within the application code. They are not referenced by the CSS theme for media queries. Set screen sizes for CSS media queries in *theme.json* located in the theme folder.  

**_questionWeight** (number): This value is used by [Question components](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#question-components) when using the function [`setScore()`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/questionView.js). This value functions as a global default for all Question components; but individual components may override it by including the same attribute in its JSON model. Reference the Matching component's [_example.json_](https://github.com/adaptlearning/adapt-contrib-matching/blob/master/example.json) as an example.

**_accessibility** (object): Adapt's built-in accessibility feature provides tab-highlighting, enables aria-labels that are otherwise hidden, and processes content text to ensure screen readers can access it. The accessibility attributes group contains values for **_isEnabled**, **_shouldSupportLegacyBrowsers**, and **_isTextProcessorEnabled**.  

>**_isEnabled** (boolean):  Specify a value of `true` or `false` to enable or to disable the accessibility feature.  

>**_shouldSupportLegacyBrowsers** (boolean):  If set to `true`, Adapt will supply the 'focused' class to accommodate some legacy browser's inability to recognize `:focus`. The 'focused' class is used to outline elements when tab-highlighting is enabled.

>**_isTextProcessorEnabled** (boolean):  If set to `true`, content text is processed by the `a11y_text` function of [_jquery.a11y.js_](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/libraries/jquery.a11y.js). The primary goal is to ensure the text or HTML is accessible by tabbing.

**_drawer** (object): Adapt's [Drawer](https://github.com/adaptlearning/adapt_framework/wiki/Core-modules#drawer) provides a slide out panel that is often used to display indicators of page level progress and links to ancillary course resources. The Drawer uses the [velocity.js](http://julian.com/research/velocity/) engine for its animations. The Drawer attributes group contains values for **_showEasing**, **_hideEasing**, and **_duration**.  

>**_showEasing** (string):  This value controls the variations in speed and bounce as the Drawer opens. It must be a [value acceptable to Velocity](http://julian.com/research/velocity/#easing). Most of [jQueryUI's easings](http://easings.net/) are built into Velocity. 

>**_hideEasing** (string):  This value controls the variations in speed and bounce as the Drawer closes. It must be a [value acceptable to Velocity](http://julian.com/research/velocity/#easing). Most of [jQueryUI's easings](http://easings.net/) are built into Velocity. 

>**_duration** (number):  Specifies the number of milliseconds it will take for the Drawer to open or close.

**_spoor** (object): Adapt's [**Spoor** extension](https://github.com/adaptlearning/adapt-contrib-spoor) provides course tracking functionality. Its attributes are detailed in its [README](https://github.com/adaptlearning/adapt-contrib-spoor).  

**_disableAnimationFor** (string array): A comma separated list of jQuery selectors that could match on the HTML tag. A match allows core modules and other plug-ins to employ alternative styles for those browsers that do not support common animation techniques. Typical strings include `".ie8"` ([*index.html*](https://github.com/adaptlearning/adapt_framework/blob/master/src/index.html)), and `".iPhone.version-7\\.0"` ([*src/core/js/device.js*](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/device.js)). 

**build** (object): By default, Adapt includes all installed plug-ins in its build process. (The result of the build is found at `build/adapt/`.) Sometimes the developer may install plug-ins that are only used during development or that are not yet being used by the content. This bloats the build needlessly. The **build** object allows the developer to specify explicitly which plug-ins will be included in the build or excluded from the build. The build attributes group is **optional**. It contains values for one of two arrays: **excludes** or **includes**.  

>**excludes** (string array):  All plug-ins will be included in the build except those whose names appear in this comma separated list.

>**includes** (string array):  Only the plug-ins whose names appear in this comma separated list will be included in the build.

>Example:  
```
"build": {
    "excludes": [
        "adapt-inspector",
        "adapt-contrib-assessmentResultsTotal"
    ]
} 
```   



   
    
   