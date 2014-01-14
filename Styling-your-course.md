Themes
------
Adapt supports user-defined themes, a special kind of plugin that lets you style your course in a variety of ways. Themes are written in [LESS](http://lesscss.org/), all CSS syntax is supported plus variables and nested rules. The HTML templates are created using [handlebars](http://handlebarsjs.com/).

A basic theme, [adapt-contrib-vanilla](https://github.com/adaptlearning/adapt-contrib-vanilla) is included in the framework. 

Simple customisation is possible by changing the built-in variable in ```less/variables.less```
#####Theme variables
######Main colours
- **@primary-color**   
- **@secordary-color**
- **@tertiary-color**
- **@foreground-color**
- **@background-color**
- **@inverted-foreground-color**
- **@inverted-background-color**
- **@transparency**

###How to modify the vanilla theme

Locate the vanilla theme located in the following directory:
``src/theme/adapt-contrib-vanilla`` here you will find all of the elements which make up an Adapt theme.

The ```/less/``` folder contains all of the style elements and it is here where we can quite quickly change the look of your course.

Open the file ``variables.less``

Modify the @primary-color & @secondary-color values to:

```
@primary-color:#3eb4e4;
@secondary-color:#1b87b2;
```

**Next** - [Developing plugins](https://github.com/adaptlearning/adapt_framework/wiki/Developing-plugins)