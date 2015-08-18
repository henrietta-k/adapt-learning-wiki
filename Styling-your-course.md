Themes
------
Adapt supports user-defined themes, a special kind of plugin that lets you style your course in a variety of ways. Themes are written in [Less](http://lesscss.org/), all CSS syntax is supported plus variables and nested rules. The HTML templates are created using [Handlebars](http://handlebarsjs.com/).

A basic theme, [adapt-contrib-vanilla](/adaptlearning/adapt-contrib-vanilla) is included in the framework's *src/theme* folder. 

The framework permits only one theme to be installed at a time. To switch to a new theme, uninstall the **Vanilla** theme, then install the new theme. Run the following commands:  
```bash
$ adapt uninstall contrib-vanilla
$ adapt install some-other-theme
$ grunt build
```

###Theme variables  
Simple customisation is possible by changing the built-in variables in **Vanilla**'s *less* folder: *colors.less*, *fonts.less*, *generic.less*, and *paddings.less*.  

####Main colors

Use variables to store your theme's colors. Assign these to roles in your color scheme. This will help achieve a consistent look and feel across your course.

- **@primary-color**

This is your theme's main color. This variable could be used for the overall color of your theme by assigning it to all UI elements such as button color or an interactive element such as an accordion background color.

- **@secondary-color**

This the the theme's secondary color. Set this variable to something that complements your primary. An example of where the secondary could be used is the hover colors.

- **@tertiary-color**

The tertiary variable is your theme's supporting color. This could be used where both primary and secondary colors are used together to style a button and a third color is now required for the hover state.

- **@foreground-color**

The foreground color is used as your content's main color. Use this to set properties such as font-color.

- **@background-color**

The background color is used in conjunction with the foreground color. An example would be text component, where if the foreground-color is white then background-color should be set as a darker color.

- **@inverted-foreground-color**
- **@inverted-background-color**

The inverted foreground/background are used in similar way as above. An ideal situation to use this is the the narrative component. The strapline background would be the inverted-background-color whilst the text would be the inverted-foreground-color. This should be used when you want an element to stand out from the background.

- **@transparency**

Transparencies are used for modal pop-ups to fade out the content underneath so the learner's focus is on the pop-up.

- **@transparency-fallback-png**

To support browsers that don't support transparent color, a fallback is required. This is set by providing a transparent PNG and setting the source of the file to this variable.

####Validation States

- **@validation-error**  
- **@validation-success**

Set a validation error color to highlight items and instruction text when the learner's input is disallowed and to color the "X" icon when the answer is incorrect. Be careful in your choice since this color needs to attract the learner's attention. Set a validation-success color to highlight the tick icon when the answer is correct.

####Device widths

These variables are used to set the breakpoints that determine what widths the design will respond to. For example **@device-width-small** could be used to set your mobile breakpoint. These are found in *less/generic.less*

####Global spacing

Set the variables for padding and margins for all titles and body text in your course in *less/paddings.less*.

####Fonts

Setup global font styling and properties in *less/fonts.less*.


###Style Rules  
Variables set in *colors.less*, *fonts.less*, *generic.less*, and *paddings.less* are assigned to CSS styles found in the various files contained in the *less/src* folder.

####Navigation

The navigation is the bar that is fixed to the top of the browser window. These CSS rules used to style the navigation bar and the icons that sit within it are located in *less/src/navigation.less*.

####Drawer

Drawer is the panel that slides out from the right of the browser window. Use the rules in *less/src/drawer.less* to style the drawer panel and the items that sit inside it.

####Notify

**Notify** includes most modal pop-ups like you see with a question's feedback. Style them with rules found in *less/src/notify.less*. 

####Icons

Styles for the SVG icons used in your theme are found in *less/src/icons.less*. An example of such an  icons would be the check-box icon that appears in a **Multiple Choice Question** (adapt-contrib-mcq). Contained in this file are the assignments of icon codes to the classnames used to represent them, for example, `.icon-tick:before {content: "\e633";}`

####Button

The styles found in *buttons.less* cover all states of a button. An example of a button in Adapt is the submit button on a question component. All the styling applied here will be applied to all buttons in the course. Make sure buttons are styled, not just for use with a mouse, but also for touch on a mobile device.

###Theme templates

Inside the *templates* folder you will find editable Handlebars templates for various views such as the page and block. 

It's important to understand how Adapt renders these templates before changing them significantly. For example, in *block.hbs*, you will find this `div` element:  
```
<div class="component-container">
</div>
```  
Removing this element or changing the class name would mean that components would no longer render.

Remember to use [Handlebars helpers](http://handlebarsjs.com/block_helpers.html) to make sure only the html that needs to be displayed is rendered.

###Theme Javascript

The theme JavaScript files found in the *js* folder should be used to add any additional theming that cannot be done using just html/css (.hbs/.less). For example, you could ass JavaScript to fade in an image when the page loads.

It's strongly recommended that the theme shouldn't be setting any attributes on [Backbone models](http://backbonejs.org/#Model-View-separation); you can, however, use classes if, say, you want an effect on a particular page.

You can use the [core events](https://github.com/adaptlearning/adapt_framework/wiki/List-of-core-events) to add an effect on, say, a page postRender event.

###Theme Assets

Place any assets required for your theme to display correctly in the *assets* folder. Any course related assets should be placed in the course folder (_src/course/en/*_) rather than here. Remember to provide smaller sized assets for mobile devices to keep page weights down.

###How to modify the **Vanilla** theme

Locate the **Vanilla** theme:  *src/theme/adapt-contrib-vanilla* Here you will find all of the elements which make up an Adapt theme.

The *less* folder contains all of the style elements, and it is here where we can quite quickly change the look of your course.

Open the file *colors.less* and create a new Less variable:  
@crimson: #DC143C;

Assign the new color variable to the `@primary-color`:  
`@primary-color: @crimson;`

Save your file, rebuild the course, and preview in your browser. Significant elements in your course now appear in red. Continue to modify the remaining variables in the *.less* file for further customisation.

**Next** - [[Developing plugins]]