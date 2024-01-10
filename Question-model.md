# Question model

The following covers Core question model functionality: [Feedback titles](https://github.com/adaptlearning/adapt_framework/wiki/Question-model#feedback-titles), [Feedback image support](https://github.com/adaptlearning/adapt_framework/wiki/Question-model#feedback-image-support).

## Feedback titles

Feedback titles tbc

***


## Feedback image support

Support for feedback images was introduced in [v6.20.5](https://github.com/adaptlearning/adapt-contrib-core/releases/tag/v6.20.5). This behaviour is fully backward compatible if the old style of `_feedback` objects are used. The new style feedback can be used in the new AAT and if building by hand, it will not be supported in the classic AAT.

Images mirror the question feedback text so there are `_feedback._correct`, `_feedback._partlyCorrectNotFinal`, `_feedback._partlyCorrectFinal`, `_feedback._incorrectNotFinal`, `_feedback._incorrectFinal` and for `_items[].feedback`.

If an image is defined, the layout of the text and image is split 60% / 40% in favour of the text. If no image is defined the text defaults to 100% width. 

The image position can be configured per feedback text via `_imageAlignment`. Options include: `left`: Image aligned to the left of the text area, `top`: Image aligned above the text area, `right`: Image aligned to the right of the text area and `bottom`: Image aligned below the text area. The default alignment is `right`.

Example `_feedback` JSON to be added to question component in _component.json_:<br>
<pre>
        "_feedback": {
          "title": "Global feedback title",
          "_classes": "",
          "_correct": {
            "altTitle": "",
            "title": "",
            "body": "Correct feedback final",
            "_classes": "",
            "_imageAlignment": "left",
            "_graphic": {
              "_src": "course/en/images/single-width.png",
              "alt": "",
              "attribution": ""
            }
          },
          "_incorrectNotFinal": {
            "altTitle": "",
            "title": "",
            "body": "Incorrect feedback not final",
            "_classes": "",
            "_imageAlignment": "right",
            "_graphic": {
              "_src": "course/en/images/single-width.png",
              "alt": "",
              "attribution": ""
            }
          },
          "_incorrectFinal": {
            "altTitle": "",
            "title": "",
            "body": "Incorrect feedback final",
            "_classes": "",
            "_imageAlignment": "left",
            "_graphic": {
              "_src": "course/en/images/single-width.png",
              "alt": "",
              "attribution": ""
            }
          }
        }
</pre>

As per other Adapt images, `alt` and `attribution` properties are supported per feedback `_graphic`.
***

