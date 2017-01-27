# *course.json*  

_course.json_ is located at [_/src/course/en/course.json_](https://github.com/adaptlearning/adapt_framework/blob/master/src/course/en/course.json). This required file is included with the installation of the Adapt framework and the Adapt authoring tool. 

>**Note**: What's the difference between _config.json_ and _course.json_?   
- _course.json_ is focused on **content** that is used throughout your course, oftentimes being reused by various components and other plug-ins. Whereas [_config.json_](https://github.com/adaptlearning/adapt_framework/wiki/Configure-your-project-with-config.json) contains settings that determine how your Adapt project **functions**.
- _course.json_ resides **inside** of the language folder (e.g., _/src/course/en_) and _config.json_ resides **outside**. Settings that are language dependent go in _course.json_.   

## Settings Overview  

Adapt employs a hierarchy of web elements to provide structure to course content: pages, articles, blocks, and components. The structure finds its root, the originating ID, in *course.json*. It supplies content that is used throughout the course and that is not specific to any particular structural element.

*course.json* begins with a group of attributes that are common to the structural elements. You'll see them often: **_id**, **_type**, **title**, **displayTitle**, **description**, and **body**. They are followed by defaults for button labels, values of [aria](http://webaim.org/techniques/aria/) regions and labels, and values for plug-ins that cross structural elements.

The properties and their values explained below found in _course.json_. Reference [_course.json_](https://github.com/adaptlearning/adapt_framework/blob/master/src/course/en/course.json) on GitHub to see them properly formatted as JSON. [_Configuration Settings_](https://github.com/adaptlearning/adapt_authoring/wiki/Configuration-settings) provides information about how they appear in the [authoring tool](https://github.com/adaptlearning/adapt_authoring/wiki). 

The order in which the properties appear in *course.json* is unimportant. And whether a group is required is often determined by whether the plug-in is being used.

### Attributes  

**_id** (string): Any value is acceptable, though `"course"` or a course code is often used.   

**_type** (string): Only one value is acceptable: `"course"`.  

**title** (string): This is the value assigned to the web document title.  

**displayTitle** (string):  Refer to your chosen menu (*example.json*, */templates/*menu*.hbs*) to see if this value is required.  

**description** (string):  Refer to your chosen menu (*example.json*, */templates/*menu*.hbs*) to see if this value is required.  

**body** (string):  Refer to your chosen menu (*example.json*, */templates/*menu*.hbs*) to see if this value is required.  

**_buttons** (object): The **buttons** group supplies label texts for the buttons used by questions. The five buttons labels (**_submit**, **_reset**, **_showCorrectAnswer**, **_hideCorrectAnswer**, **_showFeedback**) are applied to two buttons used by the core Question components. The use is governed by the configuration of the component that uses them. **_showCorrectAnswer** is enabled when **_canShowModelAnswer** is `true`. **_reset** is enabled when the value of **_attempts** is greater than 1. A third element, a text label, becomes visible when **_shouldDisplayAttempts** is `true`. It displays the values of **remainingAttemptsText** and **remainingAttemptText**. ARIA labels are not visible. They are used by assistive technology such as a screen reader when accessibility is enabled.  More detail is provided in the [*Core Buttons* wiki article](Core-Buttons). 

**_globals** (object): The **globals** group provides ARIA labels for all of Adapt's core modules and installed plug-ins. It is divided into subgroups, organizing labels for **_components**, **_extensions**, **_menu**, and **_accessibility**.  When installing a component or extension that has followed Adapt's plug-in design standards, it is recommended to add an entry to **_globals**.  

**_latestTrackingId** (number): This value is maintained by Adapt's build process and by Grunt's `--tracking-reset` task. It is used to number the blocks that are tracked by a learning management system (LMS). Under normal conditions, there is no reason to change this.  

**_start** (object): When enabled, the optional **Start Controller** group provides a way of controlling which page of the course is viewed first. It contains values for **_isEnabled**, **_startIds**, **_id**, and **_force**.  

>**_isEnabled** (boolean): This value provides a way to turn off the start page. This is convenient during development. Acceptable values include `true` and `false`.  

>**_startIds** (array):  Each object in the **start ID** group describes a start page and the conditions under which it will be chosen. When multiple pages are specified, the first one that satisfies criteria will be used. Each item in the **start ID** group has the properties **_id**, **_className** and **_skipIfComplete**.  

>>**_id** (string):  This value matches the `_id` of the page found in *contentObjects.json*.  

>>**_skipIfComplete** (boolean): If set to `true`, the page will not be selected as the first page if it has already been viewed (`"_isComplete:" true`). 

>>**_className** (string): This optional attribute provides classes that can be used to select a start page based on device width and on whether its screen is touch-enabled. Classes are assembled as a comma separated list. Values may be any combination of `.size-small`, `.size-medium`, and `.size-large`, and may include `.touch` and `.no-touch`; however, it makes no sense to include both `.touch` and `.no-touch` since they are exclusive. These values are compared against the classes in the HTML element.  

>**_id** (string): Set **_id** to the default start page. If no page represented by a **start ID** group is selected (no match on **_className** or on completion status), the course will be routed to this page ID. If you just want the default start location (the main menu) to be shown, you can leave this property out.

>**_force** (boolean): If set to `true`, this attribute will cause the course to route to the eligible start page regardless of the URL provided.

>**_isMenuDisabled** (boolean): If set to `true` and **_isEnabled** is also `true`, this will completely prevent routing to the menu page.

#### Example 1:  
Always show co-05 as the start page.
```
"_start": {
    "_isEnabled": true,
    "_id": "co-05",
    "_force": true
}
```
#### Example 2:  
Show co-05 as the start page, unless it has been completed, in which case show the main menu
```
"_start": {
    "_isEnabled": true,
    "_startIds": [
        {
            "_id": "co-05",
            "_skipIfComplete": true
        }
    ],
    "_force": true
}
```
#### Example 3:  
On small and medium touch-capable devices, always show co-05 as the start page. On small and medium devices without touch support, always show co-10 as the start page. For everything else, show the main menu as the start page.
```
"_start": {
    "_isEnabled": true,
    "_startIds": [
        {
            "_id": "co-05",
            "_skipIfComplete": false,
            "_className": ".size-small.touch, .size-medium.touch",
        },
        {
            "_id": "co-10",
            "_skipIfComplete": false,
            "_className": ".size-small.no-touch, .size-medium.no-touch"
        }
    ],
    "_force": true
}
```
#### Example 4:  
On small and medium touch-capable devices, show co-05 as the start page. For everything else, show co-10 as start page. In all browsers/devices, if a different route is specified via the URL, that will be given priority (so if you were to refresh the page whilst on co-15 you would be taken back to co-15 instead of being redirected to one of the start pages).
```
"_start": {
    "_isEnabled": true,
    "_startIds": [
        {
            "_id": "co-05",
            "_skipIfComplete": false,
            "_className": ".size-small.touch, .size-medium.touch"
        }
    ],
    "_id": "co-10"
}
```
