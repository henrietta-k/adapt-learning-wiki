The Authoring Tool now supports editable themes. This means that any theme can expose its Less variables to the Authoring Tool and they will appear on the new theme editing page. When theme settings have been modified, they can easily be saved as a preset which makes it easy to use them across multiple courses. This page describes how to get started with making an existing theme editable, so that you can start using this feature straight away!

## How to make an existing theme editable
This documentation assumes that you already have a theme and you would like to make it editable. If you do not already have a theme you will need to create this first - see https://github.com/adaptlearning/adapt_framework/wiki/Developers-Guide:-Theme for more information.


## Determine the Less variables that will be editable
To begin, you will need a list of the Less variables in your theme that you would like to expose to the Authoring Tool. Less variables start with an '@' sign. For example, in Vanilla:

```
@blue: #4287f5;
@black: #040405;
```

Editable themes must expose Less variables, so if you have a property you wish to edit that is not in a variable, you will need to convert it to a variable. For example, if your theme contains the following style and you would like it to be editable, you must modify it like so:

```
.menu-item-button {
    padding: 10px;
}
```
Becomes
```
@menu-item-button-padding: 10px;
 
 
.menu-item-button {
    padding: @menu-item-button-padding;
}
```
Now you will be able to expose @menu-item-button-padding to the Authoring Tool.



## Modify the properties.schema file
Your theme should already contain a properties.schema file. This file must be modified to include the editable variables. The properties.schema file should already contain a properties object, it will look like this:
```
{
  "type":"object",
  "$schema": "http://json-schema.org/draft-04/schema",
  "id": "http://jsonschema.net",
  "$ref": "http://localhost/plugins/content/theme/model.schema",
  "properties":{
    // SOME PROPERTIES HERE
  }
}
```

You must add a variables object into the properties object. So in order to edit @blue and @black you must make the following changes: 

* A variables object has been added. Inside this object a "_colors" object has been added - this is optional, including it will give this setting the "Colours" title as shown in the image above. Breaking settings into groups can improve the UI for themes with a large amount of editable settings.
* The "_colors" object contains properties, any exposed colour variables should be listed here. 
* The name of the variable in your Less file must match the name in the properties.schema. For example, the Less defines "@blue" so in this case the properties.schema must specify "blue".
* Title and help text will be displayed in the Authoring Tool.
* The inputType will specify the UI element that is displayed in the Authoring Tool. "ColourPicker" will open a colour palette, other valid input types are "Text" and "Asset:image". Support for more input types will be added in future releases.

```
{
  "type":"object",
  "$schema": "http://json-schema.org/draft-04/schema",
  "id": "http://jsonschema.net",
  "$ref": "http://localhost/plugins/content/theme/model.schema",
  "properties":{
    "variables": {
      "_colors": {
        "type": "object",
        "required": false,
        "title": "Colours",
        "properties": {
          "blue": {
            "title": "Blue",
            "help": "This is the blue colour used in the theme.",
            "type": "string",
            "inputType": "ColourPicker",
            "default": "#078292"
          },
          "black": {
            "title": "Black",
            "help": "This is the black colour used in the theme.",
            "type": "string",
            "inputType": "ColourPicker",
            "default": "#4b4e4f"
          }
        }
      }
    }
  }
}
```


You can add new groups of variables to your properties.schema file. So in order to make @menu-item-button-padding from above editable, you could add a new "Menu" section to your list of editable properties.
```
{
  "type":"object",
  "$schema": "http://json-schema.org/draft-04/schema",
  "id": "http://jsonschema.net",
  "$ref": "http://localhost/plugins/content/theme/model.schema",
  "properties":{
    "variables": {
      "_colors": {
        "type": "object",
        "required": false,
        "title": "Colours",
        "properties": {
          "blue": {
            "title": "Blue",
            "help": "This is the blue colour used in the theme.",
            "type": "string",
            "inputType": "ColourPicker",
            "default": "#078292"
          },
          "black": {
            "title": "Black",
            "help": "This is the black colour used in the theme.",
            "type": "string",
            "inputType": "ColourPicker",
            "default": "#4b4e4f"
          }
        }
      },
      "_menu": {
        "type": "object",
        "required": false,
        "title": "Menu",
        "properties": {
          "menu-item-button-padding": {
            "title": "Menu button padding",
            "help": "Applied to menu buttons.",
            "type": "string",
            "inputType": "Text",
            "default": "10px"
          }
        }
      }
    }
  }
}
```

## Creating editable image variables
Images can be made to be editable in much the same way as other properties, an example of this has been included below for clarity. In the below example, "mylogo.jpg" is included in the theme, and is the default image that will be displayed if this property has not been edited. When an image is editable, users of the Authoring Tool will be able to select a replacement image from the tools asset manager.

The theme must define the asset path as a variable like so:
```
@theme-logo: "assets/mylogo.jpg";
 
 
div.theme-logo {
    background-image: url("@{theme-logo}");
    background-repeat: no-repeat;
    width: 64px;
    height: 64px;
    background-size:contain;
    margin-left: 60px;
}
```


The properties.schema file must define the property as follows:
```
{
  "type":"object",
  "$schema": "http://json-schema.org/draft-04/schema",
  "id": "http://jsonschema.net",
  "$ref": "http://localhost/plugins/content/theme/model.schema",
  "properties":{
    "variables": {
      "_images": {
        "type": "object",
        "required": false,
        "title": "Images",
        "properties": {
          "theme-logo": {
            "title": "Logo",
            "help": "This is the logo image, it will be displayed on the header of every page",
            "type": "string",
            "inputType": "Asset:image",
            "default": ""
          }
        }
      }
    }
  }
}
```