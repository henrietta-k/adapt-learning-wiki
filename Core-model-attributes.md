All core models inherit from AdaptModel (adaptModel.js) and contain the following attributes:

##### _id

##### _type

##### title

##### body

##### _isComplete
Default: ``false``

##### _isEnabled
Default: ``true``

##### _isEnabledOnRevisit
Default: ``true``

##### _isAvailable
Default: ``true``

##### _isOptional
Default: ``false``

##### _isTrackable
Default: ``true``

##### _isReady
Default: ``false``

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
