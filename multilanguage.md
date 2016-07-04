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
4. A new folder named "languagefiles" is created. It contains the following files with names that reflect the options used with the `translate:export` command: *articles_export_xx.csv*, *blocks_export_xx.csv*, *components_export_xx.csv*, *contentObjects_export_xx.csv*, *course_export_xx.csv*.

### 3. Translate exported files.   
„Es führen viele Wege zum Ziel“, «il y a plus d'une façon d'accommoder un lapin», and “there's more than one way to skin a cat”, but here's just one way to get you started:  

1. Open an exported language file, such as *components_export_en.csv*, in a word processing application. While opening be sure to specify the same field separator that used during export.  
2. Translate each cell in the blank column to its right.  
3. When finished translating, delete the column of text in the original language, leaving the remaining two columns side-by-side.  
4. Rename the file, replacing the original language code with the translated language code. For example, rename the exported English language file *components_export_en.csv* to reflect a German translation *components_export_de.csv*.  

### 4. Import language files.  
As of v2.0.11 Adapt provides grunt tasks for export and import of translatable content. These commands are most easily run when using the Adapt framework as a stand-alone development environment.  

1. Place the translated language files in the *languagefiles* folder.  All five files are required even if a file did not require translation.  
2. Open a command line window (Mac's Terminal, Window's Git Bash or Command Prompt).  
3. Navigate to the root of your course to make it the current working directory.  
4. Import the translated language files by running the following command (where `xx` has been replaced with the language code of your translation):  
```
grunt translate:import --targetLang="xx" --files="articles_export_xx.csv,blocks_export_xx.csv,components_export_xx.csv,contentObjects_export_xx.csv,course_export_xx.csv"
```  
Command options:  
`--targetLang="de"`
Specify the language of the translated files.

```
--files="files="articles_export_xx.csv,blocks_export_xx.csv,components_export_xx.csv,contentObjects_export_xx.csv,course_export_xx.csv"
```
Language files separated by a comma. Replace *xx* with the language code of the translation.  

`--csvDelimiter="|"`
Specify the delimiter used in the files to be imported.  

`--masterLang="en"` 
Specify the existing master course language. Defaults to "en".  

### 4. Relink assets if required.  
Assets are not copied into the newly created course. And paths to assets found within the course JSON files are not alterred either.


give hint when grunt task is not used  
Example how to use the Authoring Tool and the Framework to create a ML course  
