The following extend the [**Backbone model**](http://backbonejs.org/#Model):  
- configModel (configModel.js)  
- lockingModel (lockingModel.js)  
- notifyModel (notifyModel.js)  
- routerModel (routerModel.js)  
- [adaptModel](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#adapt-model-attributes) (adaptModel.js)  

All core models extend **adaptModel** (adaptModel.js), and so contain its attributes:  
- [courseModel](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#course-model-attributes) (courseModel.js)  
- [contentObjectsModel](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#contentobjects-model-attributes) (contentObjectsModel.js)  
- [articleModel](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#article-model-attributes) (articleModel.js)  
- [blockModel](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#block-model-attributes) (blockModel.js)  
- [componentModel](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#component-model-attributes) (componentModel.js)  

In addition, [questionModel.js](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#question-model-attributes) extends componentModel (componentModel.js). 

An asterisk denotes that an attribute is required.  

## Adapt Model Attributes

Attribute | Description | Default value 
--------- | ----------- | -------------
`_canShowFeedback` | Allows the user to view feedback on their answer | `true`
`_classes` | Allows you to specify custom CSS classes |  `""`
`_canReset` | Controls the model's ability to reset. When set to `false`, calling `model.reset()` will return `false` and the model will not be reset. |  `true`
`_isComplete` | Whether the item has been completed | `false`
`_isInteractionComplete` |  |  `false`
`_requireCompletionOf` | The number of children within the item that the learner must complete in order for the item to be set as completed. A value of -1 requires all of them to be completed |  `-1`
`_isEnabled` | Controls the availability of the item. If ``_isEnabled`` is false, the item is disabled. | `true`
`_isResetOnRevisit` | Determines if the item should be reset to its default values upon returning |  `false`
`_isAvailable` | Controls whether the item is available in the course | `true`
`_isHidden` | Controls the display of the item. If `_isHidden` is true, the item will not be displayed | `false`
`_isOptional` | If set to `true`, the user will not be required to complete the component in order to complete the course. The completion of the component will still be tracked, but it will be ignored during any completion calculations.  | `false`
`_isVisible` | When set to 'false', this is the equivalent of applying the CSS 'visibility:hidden' | `true`
`_isLocked` | Menus and other plug-ins can set its value using `_lockType`. Reference [Locking objects with '_isLocked' and '_lockType'](Locking-objects-with-'_isLocked'-and-'_lockType')| `false`
`_questionWeight` | The weight of a particular question, which is used when calculating the score. | `1`
`_buttons` | An object to store the label values for template buttons. Buttons can then be referenced in templates using `{{{_buttons.submit}}}` | See fig.1.

**Figure 1**
``` javascript
"_buttons": { 
   "submit": "Submit", 
   "reset": "Reset", 
   "showCorrectAnswer": "ModelAnswer", 
   "hideCorrectAnswer": "My Answer" 
}
```

## Course Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_id`*   | A unique identifier. In the authoring tool, this is randomly generated.
`_type`* | The type of the particular item. Examples include `block` and `component`.
`title`*   | Used in document title.  |   
`_children`   |   | `"contentObjects"`  
`_start`   |   |   
`_isReady` | This is used to determine if the current item is ready (i.e. has been initialised). This needs to be set manually for custom components. For instance, this may be set to true post-render. | `false`
`_isA11yCompletionDescriptionEnabled `   | Disables the hidden title label that describes the state of the course to screenreader users. | `true`

## ContentObjects Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"course"`  
`_siblings`   |  | `"contentObjects"`  
`_children`   |  | `"contentObjects"`  
`_isA11yCompletionDescriptionEnabled `   | Disables the hidden title label that describes the state of the menu/page to screenreader users. `_isOptional` contentObjects default to `false`| `true`
`_onScreen`   | Attribute for attaching predefined animation to the contentObject when the element comes into view | See [documentation](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#_onscreen-documentation) below

## Article Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"contentObjects"`  
`_siblings`   |  | `"articles"`  
`_children`   |  | `"blocks"`  
`_isA11yCompletionDescriptionEnabled `   | Disables the hidden title label that describes the state of the article to screenreader users. `_isOptional` articles default to `false`| `true` 
`_onScreen`   | Attribute for attaching predefined animation to the article when the element comes into view | See [documentation](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#_onscreen-documentation) below

## Block Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"articles"`  
`_siblings`   |  | `"blocks"`  
`_children`   |  | `"components"`  
`_isA11yCompletionDescriptionEnabled `   | Disables the hidden title label that describes the state of the block to screenreader users. `_isOptional` blocks default to `false`| `true`
`_onScreen`   | Attribute for attaching predefined animation to the block when the element comes into view | See [documentation](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#_onscreen-documentation) below

## Component Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"blocks"`  
`_siblings`   |  | `"components"` 
`_isA11yComponentDescriptionEnabled `   | Disables the hidden label that provides the component description to screenreader users. They appear under the component heading and are designed to help users understand how to interact with the user interface by providing a simple name and description of its behaviour. Labels are specified in the `_globals._component[componentName].ariaRegion` | `true`
`_isA11yCompletionDescriptionEnabled `   | Disables the hidden title label that describes the state of the component to screenreader users. Useful if the component is of no interest to a screenreader user - such as an optional decorative graphic component. `_isOptional` components default to `false`| `true`
`_onScreen`   | Attribute for attaching predefined animation to the component when the element comes into view | See [documentation](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes#_onscreen-documentation) below

## Question Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_isQuestionType` | | `true`  
`_shouldDisplayAttempts` | | `false`
`_canShowModelAnswer` | | `true`
`_canShowFeedback` | | `true`
`_canShowMarking` | | `true`
`_questionWeight` | | 

## _onScreen documentation

**\_onScreen** (object): The **\_onScreen** object that contains values for **\_isEnabled**, **\_classes**, and **\_percentInviewVertical**. The **\_onScreen** feature is best used with **blocks** and **components** though it can also be used with **contentObjects** and **articles**.

**\_isEnabled** (boolean): Turns **_onScreen** functionality on and off. Acceptable values are `true` and `false`.

**\_classes** (string): CSS class name to be applied to the location that **\_onScreen** is attached to. The class name is responsible for attaching the animation, and any associated styling required, to the element and must be predefined in one of the Less files. The standard values found in Vanilla's [_animations.less](https://github.com/adaptlearning/adapt-contrib-vanilla/blob/master/less/_defaults/_animations.less) are `fade-in`, `fade-in-top`, `fade-in-bottom`, `fade-in-left`, and `fade-in-right`. The direction in each of the class names defines the animation start point, e.g. `fade-in-right` states that the animation fades in from right to left until the element sits within its natural position.

**\_percentInviewVertical** (number): This value determines the percentage on screen the element must be before the animation is triggered. The default value is `33`.

``` javascript
"_onScreen": { 
   "_isEnabled": true, 
   "_classes": "fade-in-right", 
   "_percentInviewVertical": 33
}
```