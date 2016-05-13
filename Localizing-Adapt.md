- Add a Language selector for multi language courses
- Export all the Text needed for translation
- Duplicate Courses by importing language files

## Agreed Actions/Decisions
- Framework can proceed to the Authoring Tool
- Once the functionality is added, a solution for the Authoring Tool will be developed
- Keep existing language folders (src/course/[language])
- Add a language selector upfront the course (based on [this](https://github.com/cgkineo/adapt-languageSelection) solution)
- Changing language half way through the course will reset tracking
- Show custom message and confirm button to reset tracking
- Switch text direction based on selected language
- Add support for language specific theming (e.g. html[lang="en"])
- Implement Text Export/Import functionality
- Add "translatable" property to plugin schema files
- Add missing schema files (e.g. for contentObject, articles, ...) to the Framework
- Asset Links are not changed during Export/Import Process (manual Relinking)

## Open Decisions
- Add Language picker ~~to core framework or~~ as a plugin
- Text Export/Import as grunt task ~~or adapt-cli~~ (compatibility with AT)
- File format for Text export (JSON, CSV, XML)
- AT implementation

## Brainstorming AT-implementation

MultiLanguage (ML) Bundle
- create ML courses by bundling courses into one ML-Package
- create a master course
- add LanguagePicker plugin to master course
- duplicate
- localize course
	- optionally update individual course structure
	- update assets for a language if required
- repeat for all languages
- select courses
- build "ML-course" from selected courses <-- new feature
	- build master course with Language-Picker
	- move to temp Folder
	- build each sub-language and append build/course/[lang] to master course
	- download master course
- would be good to persistently store Ml-Course bundles and mapping to sub-courses in the AT
	- will require new type of course?