Themes
------
Adapt supports user-defined themes, a special kind of plugin that lets you style your course in a variety of ways. Themes are written in [LESS](http://lesscss.org/), all CSS syntax is supported plus variables and nested rules. The HTML templates are created using [handlebars](http://handlebarsjs.com/).

A basic theme, [adapt-contrib-vanilla](https://github.com/adaptlearning/adapt-contrib-vanilla) is included in the framework. 

Simple customisation is possible by changing the built-in variable in ```less/variables.less```
#####Theme variables
######Main colors

Use the main colours to store your theme's colors. You can use the main color in combination with other variables that set colors, for example the button color. This will help achieve a consistent look and feel across your course.

- **@primary-color**

This is your theme's main color. This variable could be used for the overall color of your theme by assigning it to all UI elements such as button color or an interactive element such as an accordion background color.

- **@secondary-color**

This the the theme's secondary color. Set this variable to something that compliments your primary. An example of where the secondary could be used is the hover colors.

- **@tertiary-color**

The tertiary variable is your theme's supporting color. This could be used where both primary and secondary colors are used together to style a button and a third color is now required for the hover state.

- **@foreground-color**

The foreground color is used as your content's main color. Use this to set properties such as font-color.

- **@background-color**

The background color is used in conjunction with the foreground color. An example would be text component, where if the foreground-color is white then background-color should be set as a darker color.

- **@inverted-foreground-color**
- **@inverted-background-color**

The inverted foreground/background are used in similar way as above. An ideal situation to use this is the the accordion component. The collapsed label color would be set using the foreground/background and the expanded display text would use the inverted.

- **@transparency**

Transparencies are used for modal popups to fade out the content underneath so the learner's focus is on the popup.

- **@transparency-fallback-png**

To support browsers that don't support transparent colour, a fallback is required. This is set by providing a transparent png and setting the source of the file to this variable.

###How to modify the vanilla theme

Locate the vanilla theme from the following directory:
``src/theme/adapt-contrib-vanilla`` here you will find all of the elements which make up an Adapt theme.

The ```/less/``` folder contains all of the style elements and it is here where we can quite quickly change the look of your course.

Open the file ``variables.less``

Modify the @primary-color & @secondary-color values to:

```
@primary-color:#BE3550;
@secondary-color:#74104B;
```

Save your file, rebuild the course and preview in your browser. You should see that your course is now displaying in a red tone. Continue to modify the remaining variables in the .less file for further customisation.

**Next** - [Developing plugins](https://github.com/adaptlearning/adapt_framework/wiki/Developing-plugins)