All core models inherit from AdaptModel (adaptModel.js) and contain the following attributes:

##### _id
A unique identifier created by the authoring tool.

##### _type
The type of the particular item. Examples include ``"type":"block"`` or ``"type":"component"``.

##### title
The title text of the particular item.

##### body
The body text content of the particular item.

##### _isComplete
Default: ``false``

Determines if the item is complete.

##### _isEnabled
Default: ``true``

Controls the availability of the item. If ``_isEnabled`` is false, the item is disabled.

##### _isEnabledOnRevisit
Default: ``true``

##### _isAvailable
Default: ``true``

##### _isOptional
Default: ``false``

Specifies whether or not a particular item is required to be completed, for instance when tracking with SCORM.

##### _isTrackable
Default: ``true``

Specifies whether or not the current item can be tracked by an extension such as SCORM.

##### _isReady
Default: ``false``

This is used to determine if the current item is ready. For instance, this may be set to true post-render.

##### _questionWeight
Default: ``1``

The weight of a particular question, which is used when calculating the score.

##### buttons
Default:
```
    "buttons": {
        "submit":"Submit",
        "reset":"Reset",
        "showCorrectAnswer":"Model Answer",
        "hideCorrectAnswer":"My Answer"
    }
```

The buttons attribute stores the label values for particular buttons found throughout the framework templates. You can reference these within a template as follows:

```
<a href="#" class="button submit">
  <h6>  
    {{{buttons.submit}}} 
  </h6>
</a>
```
