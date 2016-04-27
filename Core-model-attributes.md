All core models inherit from AdaptModel (adaptModel.js) and contain the following attributes. An asterisk denotes that an attribute is required.

Attribute | Description | Default value 
--------- | ----------- | -------------
`_id`*   | A unique identifier. In the authoring tool, this is randomly generated.
`_type`* | The type of the particular item. Examples include `block` and `component`.
`title`* | The title of the particular item.
`displayTitle` | This is the title that Adapt displays when viewing a course.
`body` | The body text content of the particular item.
`_isComplete` | Whether the item has been completed. | `false`
`_isEnabled` | Controls the availability of the item. If ``_isEnabled`` is false, the item is disabled. | `true`
`_isEnabledOnRevisit` |  | `true`
`_isAvailable` |  | `true`
`_isOptional` | If set to `true`, the user will not be required to complete the component in order to complete the course. The completion of the component will still be tracked, but it will be ignored during any completion calculations.  | `false`
`_isReady` | This is used to determine if the current item is ready (i.e. has been initialised). This needs to be set manually for custom components. For instance, this may be set to true post-render. | `false`
`_isVisible` |  | `true`
`_isLocked` | Menus and other plug-ins can set its value using “_lockType”. Reference ["Locking objects with '_isLocked' and '_lockType'](Locking-objects-with-'_isLocked'-and-'_lockType')| `false`
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