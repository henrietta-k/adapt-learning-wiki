The Adapt framework provides a core set of buttons intended to be used with [question components](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#question-components).   

All question components are expected to extend [*questionView.js*](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/questionView.js). And *questionView.js* builds this core set of buttons using [*buttonView.js*](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/buttonsView.js). It, in turn, retrieves label text from the model supplied in *components.json* or, if not present there, from the defaults in *course.json*.  

The `_buttons` object stores the label values for the template `buttons.hbs`. Buttons can then be referenced in templates using this model: `{{{_buttons._submit}}}`

### Example JSON  

````
"_buttons": {
    "_submit": {
        "buttonText": "Submit",
        "ariaLabel": "Select here to submit your answer."
    },
    "_reset": {
        "buttonText": "Reset",
        "ariaLabel": ""
    },
    "_showCorrectAnswer": {
        "buttonText": "Correct Answer",
        "ariaLabel": ""
    },
    "_hideCorrectAnswer": {
        "buttonText": "My Answer",
        "ariaLabel": ""
    },
    "_showFeedback": {
        "buttonText": "Show feedback",
        "ariaLabel": ""
    },
    "remainingAttemptsText": "attempts remaining",
    "remainingAttemptText": "final attempt"
}
````  
<div float align=right><a href="#top">Back to Top</a></div>

### Attributes  

**_buttons** (object): The buttons attribute group that stores multiple button objects and the properties that govern their use. Find the template for buttons in `theme/templates/partials/buttons.hbs`.

>**_submit** (object): A button object that triggers the evaluation of a response. Contains values for
`buttonText` and `ariaLabel`.  

>>**buttonText** (string): Text that is used to label the button.  

>>**ariaLabel** (string): This text labels an element that has no visible text label. The text is read aloud by screen readers.  

>**_reset** (object): A button object that clears the learner’s selection or input. Contains values for `buttonText` and `ariaLabel`.  

>>**buttonText** (string): Text that is used to label the button.  

>>**ariaLabel** (string): This text labels an element that has no visible text label. The text is read aloud by screen readers.  

>**_showCorrectAnswer** (object): A button object that displays the correct answer. Contains values for
`buttonText` and `ariaLabel`.  

>>**buttonText** (string): Text that is used to label the button.  

>>**ariaLabel** (string): This text labels an element that has no visible text label. The text is read aloud by screen readers.  
  
>**_hideCorrectAnswer** (object): A button object that removes the correct answer from view. The opposite
behavior of _showCorrectAnswer. Contains values for `buttonText` and `ariaLabel`.  

>>**buttonText** (string): Text that is used to label the button.  

>>**ariaLabel** (string): This text labels an element that has no visible text label. The text is read aloud by screen readers.  

>**_showFeedback** (object): A button object that displays the current feedback text. Contains values for
`buttonText` and `ariaLabel`.  

>>**buttonText** (string): Text that is used to label the button.  

>>**ariaLabel** (string): This text labels an element that has no visible text label. The text is read aloud by screen readers.  

>**remainingAttemptsText** (string): This text is concatenated to the number of times a learner may submit an answer.  

>**remainingAttemptText** (string): This text is displayed when the learner is permitted to submit an answer once.     

<div float align=right><a href="#top">Back to Top</a></div>

### Button Labels  

Text values for button labels can be set in two places:  

* **course.json:**  When button values are provided in _course.json_, they will apply to all question components.   

* **components.json:** When button values are provided in _components.json_, they will override what is provided in _course.json_.  

For ease of maintenance, it is recommended that default values be set in *course.json* and that values be set in *components.json* only for those components that require different labels. Components that will use the default values in *course.json* do not need to provide button properties in *components.json*.    

#### Remaining Attempts  

Text indicating the remaining attempts is displayed by setting `_shouldDisplayAttempts` to `true`. `_shouldDisplayAttempts` is an attribute that is configured for each question component in *components.json*.
<div float align=right><a href="#top">Back to Top</a></div>

### Button Templates and Styling

Themes are expected to provide a template and CSS/Less for the buttons (typically named *buttons.hbs* and *buttons.less*, respectively). If a component provides its own *buttons.hbs,* it will be overridden by the theme's *buttons.hbs.*   

To style buttons:  
* Directly modify the theme's *buttons.hbs* and *buttons.less*,  
**OR**  
* Add a custom/bespoke class to the theme that includes the buttons' containing `div` among the selectors. Then add the class name to the component's `_classes` property. *Avoid class names already in use by the theme.*     

-----------------  
**Applies to**   
**Adapt framework:** v2.0+  
**Adapt authoring tool:** v0.2+