

[`_globals`](#_globals) and [`_accessibility._ariaLabels`](#_accessibility-_arialabels) are found in *src/course/en/course.json* in the Adapt framework. They are configured in the Adapt authoring tool in the Project configuration menu. 

### `_globals`

`_globals` are used by assistive technology such as screen readers. They provide a description a plug-in's basic function and guidance about how to access its content. They are enabled when Adapt's accessibility feature is activated by the learner, but they are never visible. They are instead announced by a screen reader. 

Developers are encouraged to access `"_globals"` in their plug-in templates and to provide model text in their *example.json* or *README.md*. Course authors are encouraged to add the text to `"_globals"` in the appropriate location of *course.json*. (When using the Adapt authoring tool, plug-ins should expose their `"aria-label"` in the Project configuration menu.)  

These values rarely require editing, but they are exposed in case a course author feels the learner can benefit from a different description. 

```
"_globals": {
        "_components": {
            "_accordion": {
                "ariaRegion": "This component is an accordion comprised of collapsible content panels containing display text. Select the item titles to toggle the visibility of these content panels."
            },
            "_blank": {
                "ariaRegion": ""
            },
            "_gmcq": {
                "ariaRegion": "This component is a graphical multiple choice question. Once you have selected an option select the submit button below."
            },
            "_graphic": {
                "ariaRegion": ""
            },
            "_hotGraphic": {
                "ariaRegion": "Below is a component which allows you to select hot spots over an image. Select a hot spot to trigger a popup that includes an image with display text. Select the close button to close the popup."
            },
            "_matching": {
                "ariaRegion": "This question component requires you to select the matching answer from a drop down list below. When you have selected your answers select the submit button."
            },
            "_mcq": {
                "ariaRegion": "This component is a multiple choice question. Once you have selected an option select the submit button below"
            },
            "_media": {
                "ariaRegion": "This is a media component which plays a video. Select the play / pause button to watch or listen. Alternatively you can select the link below for the transcript."
            },
            "_narrative": {
                "ariaRegion": "This component displays an image gallery with accompanying text. Use the next and back navigation controls to work through the narrative."
            },
            "_slider": {
                "ariaRegion": "This component requires you to answer the question by selecting the relevant value. After selecting a value select the submit button below."
            },
            "_text": {
                "ariaRegion": ""
            },
            "_textInput": {
                "ariaRegion": "This question component requires you to input your answer in the textbox provided. When you have answered the question select the submit button below."
            }
        },
        "_extensions": {
            "_pageLevelProgress": {
                "pageLevelProgress": "Page sections",
                "pageLevelProgressEnd": "You have reached the end of the list of page sections.",
                "pageLevelProgressIndicatorBar": "Progress bar. Select here to view your current progress, and select an item to navigate to it. You have completed ",
                "pageLevelProgressMenuBar": "You have completed ",
                "optionalContent": "Optional Content"
            }
        },
        "_menu": {
            "_boxmenu": {
                "ariaRegion": "Menu",
                "menuItem": "Menu item.",
                "menuEnd": "You have reached the end of the menu."
            }
        },
```  

### `_accessibility _ariaLabels`

The aria-labels in this section of *course.json* are for various modules and elements built into the Adapt framework. Like the "_globals", these, too, rarely require editing. They are exposed in case a course author feels the learner can benefit from a different description. 

```
        "_accessibility": {
            "_accessibilityToggleTextOn": "Turn accessibility on?",
            "_accessibilityToggleTextOff": "Turn accessibility off?",
            "_accessibilityInstructions": {
                "touch": "Usage instructions. Use swipe right for next. Use swipe left for previous. Use a double tap to select. Use a two finger slide up to go to the top of the page.",
                "notouch": "Usage instructions. Use tab for next. Use shift tab for previous. Use enter to select. Use escape to go to the top of the page.",
                "ipad": "Usage instructions for touchscreens. Use swipe right for next. Use swipe left for previous. Use a double tap to select. Use a two finger slide up to go to the top of the page. Usage instructions for keyboard access. Use right for next. Use left for previous. Use up and down together to select."
            },
            "_ariaLabels": {
                "navigation": "Course navigation bar",
                "menuLoaded": "Menu Loaded.",
                "menu": "Menu",
                "page": "Page",
                "pageLoaded": "Page Loaded.",
                "pageEnd": "You have reached the end of the page.",
                "previous": "Back",
                "navigationBack": "Navigate back",
                "navigationDrawer": "Open course resources.",
                "close": "Close",
                "closeDrawer": "Close Drawer",
                "closeResources": "Close resources",
                "resourcesEnd": "You have reached the end of the list of resources.",
                "drawerBack": "Back to drawer",
                "drawer": "Top of side drawer",
                "closePopup": "Close popup",
                "next": "Next",
                "done": "Done",
                "complete": "Completed",
                "incomplete": "Incomplete",
                "incorrect": "Incorrect",
                "correct": "Correct",
                "locked": "Locked",
                "accessibilityToggleButton": "By selecting this button you can set whether accessibility is turned on or off",
                "feedbackPopUp": "Popup opened.",
                "menuBack": "Back to menu",
                "visited": "Visited"
            }
        }
    },
```

[### Read more about accessibility in Adapt.]() 