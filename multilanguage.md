>Note: The title and URL of this page *will* change.  

Chuck's questions: 
- What is the purpose of export_en.json?
- Does an LMS record as a single course regardless of language chosen?
- How does an LMS respond if the components in each language are no equal in arrangement?  

##Introduction  
With Adapt you can localise your content and engage learners in ways that speak from their native culture. Localisation may involve modifying  
- content language
- content data formats used with dates, currency, and units of measure  
- content examples, regulations and legal requirements  
- visual elements such as graphics, design and layout  

Fundamental to localisation is language, so much of the following instruction focuses on providing content in multiple languages.

Adapt (v2.0.11) provides two features to support for multiple languages:  
- language picker: Component that presents a list of available languages and allows the learner to choose which she would prefer to work in. Component can be configured to appear before entering the course content and/or while the course is in progress. 
- import/export: Commands that can be executed with Grunt. Export commands copy translatable fields into several CSV files to be used in preparing a translation. Import commands load translated content from CSV files matching the export format. 

## Language Picker  
- What it does
- What it assumes
    - localized content (Adapt does not automatically translate)
    - use of language folder in the course root
    - LMS (see questions above)

## Export/Import  
- What it does  
- What it assumes  
    - the content of imported files will only use plug-ins that are present in the src directory

## Overview of language localisation  
1. Create course in first language.  
2. Export language files.  
3. Translate exported files.
4. Import language files.
5. Relink assets if required.
6. Add the Language Picker plug-in. 

## How to recreate your course in another language

### 1. Create your course in the first language.  
Finalise the JSON content of your master course. Do not overlook titles that might be hidden in the Drawer or in the alt attribute of images.

### 2. Export language files.  
As of v2.0.11 Adapt provides grunt tasks for export and import of translatable content. These commands are most easily run when using the Adapt framework as a stand-alone development environment.

1. Open a command line window (Mac's Terminal, Window's Git Bash or Command Prompt).  
2. Navigate to the root of your course to make it the current working directory.  
3. Export the translatable fields (course JSON, global ARIA fields, etc.) by running the following command:  
`grunt translate:export --format="csv"`  
Command options:  
`--format="[csv|raw]"`
Choose the format of exported files.   
`--csvDelimiter="|"`
Specify the delimiter used to separate fields in the CSV tables. Use a character that is unlikely to appear in the content being exported.  
`--masterLang="en"` Defaults to "en". Specify the existing course language folder to be exported.
4. A new folder named "languagefiles" is created. It contains the following files with names that reflect the options used with the translate:export command: articles_export_xx.csv, blocks_export_xx.csv, components_export_xx.csv, contentObjects_export_xx.csv, course_export_xx.csv.



give hint when grunt task is not used  
Example how to use the Authoring Tool and the Framework to create a ML course  
