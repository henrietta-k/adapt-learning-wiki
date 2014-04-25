Themes
------
Adapt supports user-defined themes, a special kind of plugin that lets you style your course in a variety of ways. Themes are written in [LESS](http://lesscss.org/), all CSS syntax is supported plus variables and nested rules. The HTML templates are created using [handlebars](http://handlebarsjs.com/).

A basic theme, [adapt-contrib-vanilla](/adaptlearning/adapt-contrib-vanilla) is included in the framework and can be found in the ```theme``` folder 

To switch to a new theme, do the following:
```bash
$ adapt uninstall contrib-vanilla
$ adapt install some-other-theme
$ grunt build
```

Simple customisation is possible by changing the built-in variables in ```less/variables.less```

###Theme variables
####Main colors

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

####Validation error

- **Validation error color**

Use the variables to set a validation error color to items and instruction text. Be careful with what color you set these too since this needs to be clearly visible.

####Item setup

Use the these variables to style component items. A component item is an interactive element, e.g. a multiple choice question option. The variables are applied to every component to help achieve a consistent look to the course.

- **Item color**

Item color variables cover all the states an item can have such has a hover or selected.

- **Item border**

Similar to item color, use these variables to change how item's border styling.

- **Item padding**
- **Item spacing**

Use these variables to adjust the layout of items. 

####Button

Much like the item variables, these variables cover all states of a button. An example of a button in Adapt is the submit on a question component. Again like the item all the styling applied here will be applied to all buttons in the course.

Make sure buttons are styled, not just for use with a mouse but also for touch on a mobile device.

####Device widths

These variables are used to set the breakpoints in Adapt. For example **@device-width-small** could be used to set your mobile breakpoint.

####Global spacing

Use these variables to set the padding and margins for all titles and body text in your course.

####Navigation

The navigation is the bar that is fixed to the top of the browser window. These variables are used to style the navigation bar and the icons that sit inside it.

####Drawer

Drawer is the panel that slides out from the right of the browser window. These variables are used to style the drawer panel and the items that sit inside it.

####Notify

The variables here apply styling to all notify popup's in your course. This can include popup's like question feedback.

####Fonts

Setup global font styling and properties here.

####Icons

These variables style the SVG icons in your course. Example of one of these icons would be the mcq radio icon. 

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

**Next** - [[Developing plugins]]