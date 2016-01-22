We need to start using xAPI for tracking our learning in Adapt (because it's the future!).

Some work has been done already (see [ABU-1116](https://adaptlearning.atlassian.net/browse/ABU-1116))

## Discussion Topics
#####2015
* ~~review current progress and plan of attack~~
* ~~Maintain existing spoor plugin for backwards compatibility?~~
* ~~Port event capture code from spoor to core framework?~~
* Review events fired by components/extensions/framework - 
  * Are we triggering what we need to? 
  * Are events consistent?
* ~~xAPI extension? (new Scorm one too?)~~
* Additional tracking types - in addition to SCORM/xAPI?

## Tentative Actions/Conclusions:
#####2015
* ~~Serialization should stay within the protocol (SCORM, xAPI, etc.)~~
* ~~Stateful session will move to adapt core~~
* Possibility of implementing one tracking query that each protocol can query to determine the tracking status (rather than a lot of individual tracking calls to core)

## Concrete Actions/Decisions
#####2016-01-22
* Create xAPI extension as an alternative to SPOOR - Learning Pool Team
* Allow LRS connection through query string or config.json - Learning Pool Team
* Serialization should stay within the protocol (SCORM, xAPI, etc.) - All
* Stateful session will move to adapt core - Ollie
* Create xAPI version of suspend data using the state API - Learning Pool Team
* Convert existing spoor plugin to use moved stateful session code - Ollie

## Deferred Decisions
#####2016-01-22
* Statement API style (verbs, objects etc)
* Agent profile API style and uses
* Activity profile API uses and style