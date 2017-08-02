The following extend the [**Backbone model**](http://backbonejs.org/#Model):  
- configModel (configModel.js)  
- lockingModel (lockingModel.js)  
- notifyModel (notifyModel.js)  
- routerModel (routerModel.js)  
- adaptModel (adaptModel.js)  

All core models extend **adaptModel** (adaptModel.js), and so contain its attributes:  
- courseModel (courseModel.js)  
- contentObjectsModel (contentObjectsModel.js)  
- articleModel (articleModel.js)  
- blockModel (blockModel.js)  
- componentModel (componentModel.js)  

In addition, questionModel (questionModel.js) extends componentModel (componentModel.js). 

An asterisk denotes that an attribute is required.  

## Adapt Model Attributes

Attribute | Description | Default value 
--------- | ----------- | -------------
`_canShowFeedback` |  | `true`
`_classes` |  |  `""`
`_canReset` |  |  `false`
`_isComplete` | Whether the item has been completed. | `false`
`_isInteractionComplete` |  |  `false`
`_requireCompletionOf` |  |  `-1`
`_isEnabled` | Controls the availability of the item. If ``_isEnabled`` is false, the item is disabled. | `true`
`_isResetOnRevisit` |  |  `false`
`_isAvailable` |  | `true`
`_isOptional` | If set to `true`, the user will not be required to complete the component in order to complete the course. The completion of the component will still be tracked, but it will be ignored during any completion calculations.  | `false`
`_isVisible` |  | `true`
`_isLocked` | Menus and other plug-ins can set its value using “_lockType”. Reference [Locking objects with '_isLocked' and '_lockType'](Locking-objects-with-'_isLocked'-and-'_lockType')| `false`
`_questionWeight` | The weight of a particular question, which is used when calculating the score. | `1`
`_buttons` | An object to store the label values for template buttons. Buttons can then be referenced in templates using `{{{_buttons.submit}}}` | See fig.1.

**Figure 1**
``` javascript
"_buttons": { 
   "submit":"Submit", 
   "reset":"Reset", 
   "showCorrectAnswer":"ModelAnswer", 
   "hideCorrectAnswer":"My Answer" 
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

## ContentObjects Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"course"`  
`_siblings`   |  | `"contentObjects"`  
`_children`   |  | `"contentObjects"`  

## Article Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"contentObjects"`  
`_siblings`   |  | `"articles"`  
`_children`   |  | `"blocks"`  

## Block Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"articles"`  
`_siblings`   |  | `"blocks"`  
`_children`   |  | `"components"` 
`_sortComponents`   |  | `true` 

## Component Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_parent`   |  | `"blocks"`  
`_siblings`   |  | `"components"`  


## Question Model Attributes  

Attribute | Description | Default value 
--------- | ----------- | -------------
`_isQuestionType` | | `true`  
`_shouldDisplayAttempts` | | `false`
`_canShowModelAnswer` | | `true`
`_canShowFeedback` | | `true`
`_canShowMarking` | | `true`
`_questionWeight` | | 