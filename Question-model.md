# Question model

The following covers Core question model functionality: [Feedback image support](https://github.com/adaptlearning/adapt_framework/wiki/Question-model#feedback-image-support).

## Feedback image support

Support for feedback images was introduced in [v6.20.5](https://github.com/adaptlearning/adapt-contrib-core/releases/tag/v6.20.5). Images mirror the question feedback text so there are correct, partly correct not / final, and incorrect not final versions. 

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

