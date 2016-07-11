## Start controller

The start controller allows you to choose a page that the learner will load into when they start a course.

    "_start": {
        "_isEnabled": true,  // default true, a useful attribute that allows you to turn off for debugging
        "_startIds": [
            {
                "_id": "co-00",  // used to assign the starting page.
                "_skipIfComplete": true // If the learner has accessed the page already skip
            }
        ],
        "_force": false
    },

