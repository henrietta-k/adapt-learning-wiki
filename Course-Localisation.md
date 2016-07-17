##Contents  
* [Introduction](#introduction)  
* [How to recreate your course in another language](#how-to-recreate-your-course-in-another-language)  
* [Styling localised courses](#styling-localised-courses)  
* [Building localised courses](#building-localised-courses)


##Introduction  
With Adapt you can localise your content and engage learners in ways that speak from their native culture. Localisation may involve modifying  
- content language
- content data formats used with dates, currency, and units of measure  
- content examples, regulations and legal requirements  
- visual elements such as graphics, design and layout  

Fundamental to localisation is language, so much of the following instruction focuses on providing content in multiple languages. Adapt (v2.0.11) provides two features to support for multiple languages: **Export/Import** and the **Language Picker**.  

### Export/Import  
- Adapt provides export and import functionality via the command line. Export commands copy translatable fields into several CSV files to be used in preparing a translation. Import commands load translated content from CSV files matching the export format.  
- As of v2.0.11 Adapt provides grunt tasks for export and import of translatable content. These commands are most easily run when using the Adapt framework as a stand-alone development environment.  
- Do not confuse this with exporting and importing completed courses. These techniques focus on exporting and importing texts, not entire courses. 
- Not all fields are exported for translation. Exported fields are marked as translatable in the plug-in's *properties.schema* file. Plug-ins that have no *properties.schema* will have no fields exported for translation.  
- Imported content relies on the presence of required plug-ins. The import process does not install plug-ins expected by the various language files. 
- Imported files must match the format produced by exporting translatable content. 

### Language Picker  
- The [Language Picker (adapt-contrib-languagePicker)](https://github.com/adaptlearning/adapt-contrib-languagePicker) is an extension that presents a list of available languages. It allows the learner to choose the language of the course content. The component can be configured to appear before entering the course content and/or while the course is in progress. 
- The Language Picker does not create localised content. It must be configured to reflect the languages present in the course root. 
- The Language Picker expects that Adapt conventions will be follow, specifically that localised content will be stored in a folder within the course directory and that it use the language code as the name folder.  
<div float align=right><a href="#top">Back to Top</a></div>  

## How to recreate your course in another language

### Overview of language localisation  
[1. Create course in first language.](#1-create-your-course-in-the-first-language)  
[2. Export language files.](#2-export-language-files)  
[3. Translate exported files.](#3-translate-exported-files)  
[4. Import language files.](#4-import-language-files)  
[5. Relink assets if required.](#5-relink-assets-if-required)  
[6. Add the Language Picker plug-in.](#6-add-the-language-picker-plug-in)  

### 1. Create your course in the first language.  
Finalise the JSON content of your master course. Do not overlook titles that might be hidden in the Drawer or in the `alt` attribute of images.

### 2. Export language files.  
>**Note**: Only those text fields marked as "translatable" will be exported. Fields are so designated in properties.schema. Read more about [Properties Schema](https://github.com/adaptlearning/adapt_authoring/wiki/Properties-Schema).   

As of v2.0.11 Adapt provides grunt tasks for export and import of translatable content.  

1. Open a command line window (Mac's Terminal, Window's Git Bash or Command Prompt).    
2. Navigate to the root of your course to make it the current working directory.  
3. Export the translatable fields (course JSON, global ARIA fields, etc.). To export from *course/en* into a CSV file format, run the following command:  
`grunt translate:export --format="csv"`  

    **Command model:**  
    `grunt translate:export [--masterLang=en] [--format=json|raw|csv] [--csvDelimiter=,]` 

    **Command options:**  
    `--masterLang="en"` Specify the existing course language folder to be exported. Defaults to "en".  
    `--format="[json|csv|raw]"` Choose the format of exported files. Defaults to "json".    
    `--csvDelimiter=","` Specify the delimiter used to separate fields in the CSV tables. Use a character that is unlikely to appear in the content being exported. Defaults to ",".  
 
4. A new folder named "languagefiles" is created with a subfolder named with the value of `masterLang`. The subfolder contains the following files with names reflecting the options used with the `translate:export` command: *articles_export_xx.csv*, *blocks_export_xx.csv*, *components_export_xx.csv*, *contentObjects_export_xx.csv*, *course_export_xx.csv*.  
<div float align=right><a href="#top">Back to Top</a></div>  

### 3. Translate exported files.   
„Es führen viele Wege zum Ziel“, «il y a plus d'une façon d'accommoder un lapin», and “there's more than one way to skin a cat”, but here's just one way to get you started:  

1. Open an exported language file, such as *components_export_en.csv*, in a word processing application. While opening be sure to specify the same field separator that used during export.  
2. Translate each cell in the blank column to its right.  
3. When finished translating, delete the column of text in the original language, leaving the remaining two columns side-by-side.  
4. Rename the file, replacing the original language code with the translated language code. For example, rename the exported English language file *components_export_en.csv* to reflect a German translation *components_export_de.csv*.  

### 4. Import language files.  
As of v2.0.11 Adapt provides grunt tasks for export and import of translatable content.  
1. In the *languagefiles* folder, create a subfolder named with the language code of the translation language. For example, if the language of your original course was English (*course/en*) and you are creating a version in German (target language), create a subfolder named "de" (*languagefiles/de*). 
2. Place the translated language files in the newly created subfolder. All five files are required even if a file did not require translation.  
3. Open a command line window (Mac's Terminal, Window's Git Bash or Command Prompt).  
4. Navigate to the root of your course to make it the current working directory.  
5. Import the translated language files. To import German language files into a project configured with English as its master language, run the following command:  
`grunt translate:import --targetLang="de" --replace`  

   **Command model:**  
    `grunt translate:export [--masterLang=en] [--format=json|raw|csv] [--csvDelimiter=,] [--replace]` 

   **Command options:**  
    `--targetLang="xx"` Specify the language of the translated files.  
    `--masterLang="xx"`  Specify the existing master course language. Defaults to "en".  
    `--csvDelimiter="x"` Specify the delimiter used in the files to be imported. Defaults to ",".  
    `--replace` Overwrite an existing folder named with the value of `targetLang` e.g., an existing *course/de* folder. 

>**Note**: `--masterLang` is required if the master course is not *course/en*. `--csvDelimiter` is required if the field delimiter is not ",". `--replace` is required if the targeted language folder already exists.    

<div float align=right><a href="#top">Back to Top</a></div>  

### 5. Relink assets if required.  
Assets are not copied into the newly created course when using `grunt translate:import`. And paths to assets found within the exported course files are not altered either. This allows the developer to choose to maintain a single copy of assets or to copy all or some assets. If any assets are copied into the newly created course, paths to these assets must be updated in the appropriate files. Remember to review your theme's CSS and Less files for paths that need to be updated. 

### 6. Add the Language Picker plug-in. 
The value of the `_defaultLanguage` property in the *course/config.json* file determines which language is presented to the learner. To pass control to the learner, install [*adapt-contrib-languagePicker*](https://github.com/adaptlearning/adapt-contrib-languagePicker). The Language Picker appears before the course and allows the learner to choose the language of the course.  

>**Note:** The *languagefiles* folder and its contents may be deleted after a successful import.

## Styling localised courses

Adapt sets the `lang` attribute of the HTML element to the proper language code. CSS styles can use the [:lang( ) pseudo-class selector](http://www.w3schools.com/cssref/sel_lang.asp) to vary styles based on language.  
```CSS
// Example of styles that target the value of the lang attribute  
:lang(de) {
  body {
    font-family: Verdana;
  }
}

:lang(fr) {
  body {
    font-family: Serif;
  }
}

:lang(it) {
  body {
    font-family: monospace;
  }
}
```  
<div float align=right><a href="#top">Back to Top</a></div>  

## Building localised courses  

By default all language folders are built with the `grunt build` command. As of v2.0.11 the Adapt framework allows you to specify which languages to build. Use the `--languages` flag to specify an individual language or a subset of languages separated by a comma. To build just the German and French versions of a course, run the following command:   
`grunt build --languages=“fr,de”`


## Resources  
https://www.w3.org/International/ The W3C Internationalization (I18n) Activity