On August 3, 2015, v2.0 of the framework was released. It included some breaking changes, so courses created in v1 will not necessarily run in v2 without some conversion. The conversion process involves creating a new v2 course and transferring JSON content from the older course to the newer course.

## To convert a course from version 1 to version 2:

1. Make a backup copy of your v1 course.

2. Ensure you have installed the latest version of the adapt-cli. To update globally, run:  
`npm update -g adapt-cli`

3. Create a version 2 course by running the following command:  
`adapt create course "My Course"` where `"My Course"` is the name of your course&mdash;*do not overwrite your v1 course!*
Once the course is created, run `grunt build` as usual and verify the sample course runs by running `grunt server`.

4. Construct the version 2 course JSON files by referencing the version 1 files: *config.json*, *course.json*, *contentObjects.json*, *articles.json*, *blocks.json*, and *components.json*. While each file may have sections that can be copied and pasted into place, it is unlikely that the entire file can be copied. (If your course has no assessments and does not use Trickle, you may get lucky with *articles.json* and *blocks.json*.) Until you are familiar with the version 2 plug-ins, it is recommended that you paste into place the JSON from *examples.json*, then configure it to your needs and transfer the content. 

While this list is not comprehensive, the following are some things to watch for in each file.

#### config.json
* little has remained the same  
* here's where to configure Spoor, Right-to-Left display, accessibility, default weight for questions, default language, and drawer behavior

#### course.json
* There are completely new sections for buttons used with questions, texts used globally with accessibility, Page Level Progress, Assessment, and Bookmarking. The section for Resources has remained the same.

#### contentObjects.json
* two new properties:`pageBody` and `linkText`

#### articles.json
* While the properties proper to an article (the article model) have not changed, some of the properties of extensions that are *applied* to the article have changed. Assessment and Trickle are perhaps the most notable examples.

#### blocks.json 
* While the properties proper to a block (the block model) have not changed, some of the properties of extensions that are *applied* to the block have changed. Trickle is perhaps the most notable example.

#### components.json
* All [question components](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#question-components) have been updated to use [core buttons](https://github.com/adaptlearning/adapt_framework/wiki/Core-Buttons). No question component JSON from a course created in version 1 can be copied entirely into a version 2 course without modification.
* All components&mdash;both presentation and question&mdash;have been updated to meet WAI AA standards for accessibility. If you are using a custom component or other plug-in, it is recommended to review accessibility as it applies to its construction.
* [Presentation components](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#presentation-components) with new properties: Accordion, Graphic, Narrative, Hot Graphic, and Media. 

## More Tips for Converting Content
* (Add your tips here in this bulleted list.)
