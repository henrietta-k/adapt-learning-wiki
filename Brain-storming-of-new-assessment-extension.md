This document is intended to document the discussions around a replacement for adapt-contrib-assessment as discussed at the Adapt Hack.

Requirements:
- **Course-wide** 

Assessment should apply course-wide, as opposed to on an article.  This would allow dispersing questions over several pages.  Technically this is a better match for the Adapt Authoring tool as well.

- **Question banking**

It should be possible to assign any number of question components to associated banks of questions.  These could then be selected something like two questions from Bank A, one from Bank B, and so on.

- **Randomisation**

In conjunction with banking, it should be possible to randomise the appearance and ordering of questions.

- **Retry options**

Properties should allow configuration of the number of retry attempts a user may have.

TODO
- Question picker/placeholder component
- ...

**Example data**
In course.json (or perhaps new file extensions.json)

```json
"_diffuseAssessment":{
	"_isEnabled": true,
	"_useQuestionPickers": false,
	"_saveScoreToLMS": false,
	"_banks": [
		{
			"_id": 1,
			"_title":  "I am bank number 1"

		},
		{
			"_id": 2,
			"_title":  "I am bank number 2"
		}
	]
}
```
Create new component (questionPicker) to facilitate selection of randomised banked questions. Simple component that loads in randomised assessment
question based on data settings.

**Sample data in components.json**

```json
{
    "_id": "c-150",
    "_parentId": "b-10",
    "_type":"component",
    "_layout":"left",
    "_component":"questionPicker",
    "_isAssessment": true,
    "_question": {
        "_bankID":2, 
        "_useRandom": true,
        "_questionID": "c-95"
    }
}
```
"_bankID", "_useRandom" and "_questionID" are mutually exclusive
- specify "_bankID" if question is to be pulled from a specific bank
- specify "_useRandom" if question is to be randomly pulled from total pool of diffuse assessment questions (no banks)
- "_questionID" - not sure if this is required. Original idea was that we would replace with a specified question, but then we could just replace
with the entire question object??

The actual question data would be adjusted slightly. 
- "_parentId" wouldn't need to be specified as would inherit property from the questionPicker property (when used)
- "_diffuseAssessment" - Boolean to enable enable assessment question count if not using question pickers/randomised questions
- "_questionBankId" - assign question to a bank id specified in course.json (or extensions.json)

```json
{
	"_id":"c-195",
	"_parentId":"",
	"_type":"component",
	"_component":"gmcq",
	"_diffuseAssessment": true,
	"_questionBankId": 2,
	...
}
```
