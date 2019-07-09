### Overview

In this guide we'll be looking at a type of plug-in for Adapt called theme. Themes change the look and feel of your Adapt course. They contain Less, templates, Javascript, fonts and assets. 

The structure of an Adapt-compatible theme is as follows:  

| Folder        | Purpose|
| ------------- |:-------------|
| assets        | _Holds any static assets (for example: images, etc.)_|
| fonts         | _Any fonts which might be referenced in the associated .less files_      |   
| js            | _JavaScript/JQuery files on which the theme depends go here_      |
| less          | _Location for any [Less](http://lesscss.org/) based CSS files_ |
| templates     | _Location for any snippets of pre-defined HTML templates (see below)_ |  


Adapt themes support customisation for the rendering of various Adapt elements via the following [Handlebars](http://handlebarsjs.com/) templates.  Note that the template names are coordinated with the appropriate javascript file name:  
* article.hbs
* block.hbs
* loading.hbs 
* navigation.hbs
* page.hbs

Until this guide can be completed, please take a look at the technique explained in [Modifying the Vanilla Theme](https://github.com/adaptlearning/adapt_authoring/wiki/Modifying-the-Vanilla-Theme).

If you already have a theme, and you would like to make it work with the Authoring Tool's editable themes feature, please see [Making an existing theme editable](https://github.com/adaptlearning/adapt_framework/wiki/Making-an-existing-theme-editable).

_TO DO: Add explanation of how to use `"_classes"` by adding a CSS class to *theme-extras.less* or other Less file._