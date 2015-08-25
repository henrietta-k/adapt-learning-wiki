**DRAFT**

<img src="https://github.com/adaptlearning/documentation/blob/master/04_wiki_assets/adapt_framework/deep-scroll01.png" alt="" align="right">So what is the Adapt Framework?

You can read the full detail on the [community site](http://community.adaptlearning.org) (start with the Vision).

The Framework is a JavaScript client-side application that delivers Responsive e-learning.

E-Learning content is defined in JSON files which are included into a package along with various components or plugins.  The Adapt Framework takes these JSON files, applies them to the included components and builds Responsive HTML5 pages using them.

The Framework has a component based architecture. There is a small core with most functionality delivered by [Adapt Plugins](plugins).  Most plugins will be **Components** which produce output as part of a course.

Version 2.0 of the Framework launches with a set of [core components](Core-Components-in-the-Adapt-Learning-Framework#components)

As a developer you shouldn't normally need to modify code in the core framework. Instead, most of your time will be spent developing [Themes](plugins#theming), [Components](plugins#components) and additional plugins.

## Content Structure

<img src="https://github.com/adaptlearning/documentation/blob/master/04_wiki_assets/adapt_framework/a-b-c_structure.png" alt="diagram of boxes showing page surrounding article surrounding block surrounding component" align="right">There's some detailed information about [content structure](https://community.adaptlearning.org/mod/page/view.php?id=20) on the Community Site.

The Adapt Framework deals with "Courses".  Each package contains a single **Course** and that course is made up of **Pages**.  Pages have a hierarchical structure of **Articles** which contain **Blocks** which contain **Components**

There are rules about how these elements are tied together, and you can read about that on the [content format](wiki/content-format) page. The Components in this context are the [components](wiki/components) defined above.

## Packaging and Publishing

 