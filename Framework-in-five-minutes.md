If you're new to the Adapt framework, or the project in general, this page will provide the background you need to get started.

## What is the Adapt framework?

In a single (albeit verbose) sentence, the Adapt framework is:<br>
***a modular, reusable codebase for developing single-version, easily localisable, responsive e-learning courses***.

What this means in practice:

**Multi-device delivery**: The framework offers the cross-platform and cross-browser versatility that you expect from standard web pages, so a single build of your course will work across all devices in the [supported tech spec](https://github.com/adaptlearning/documentation/blob/master/01_cross_workstream/developer_requirements.md). With mobile devices quickly becoming the de facto way to access the web, Adapt provides a future-proof solution.

**Single source**: Keeping content current becomes less problematic when there's only one version to maintain.

**Single-page app**: Rather than force the user to download lots of pages individually, we've chosen to create Adapt as [single-page app](https://en.wikipedia.org/wiki/Single-page_application), meaning less HTTP requests, and a much more responsive experience for users, especially those on mobile or with poor data connections.

**Designed for e-learning**: Built from the ground up specifically for e-learning, the framework comes bundled with a number of useful plugins, including learner progress tracking, customisable assessments and a learning resources 'drawer'.

**Accessibility out-of-the-box**: Courses created in the Adapt framework are fully accessible with no need for a separate version to comply with DDA guidelines.

**Easily localisable**: Content can be exported from the framework to a CSV file, translated, then imported back in. A language picker allows learners to easily choose and switch languages. Find out more in the [[Course Localisation|Course-Localisation]] Wiki page

**Free**: All source code for the framework and core bundle of plugins are available for download free ([as in speech](https://en.wikipedia.org/wiki/Free_and_open-source_software)) on our GitHub page, for you to take and modify as you like.

You can check out our [complete vision statement](https://github.com/adaptlearning/documentation/blob/master/01_cross_workstream/vision_breakdown.docx) for more.

## Adapt :heart: learning design

Adapt isn’t just an e-learning framework for developers, it also offers a variety of fresh ideas and options for learning designers to create exciting new content for web savvy audiences.

**No more templates**: Ditching the rigid, template-based design of the past, Adapt pages are constructed by combining a wide range of interactive components in a flexible two-column layout capable of crafting much more complex learning paths.

**Web-inspired navigation**: No longer is page content limited by screen capacity; Adapt's scrolling page layout gives the learning designer control over how their courses should be navigated.

**Configuration**: Flexibility is at the core of Adapt; layouts, styling and a whole heap of behavioural options are configurable without needing to touch code, allowing you to completely customise courses to just how *you* want them.

### Tailoring the content to the device

Responsive e-learning design is more than having the ability to present an entire course on a variety of different devices; it’s also about having total control of what content is shown on each different platform.

Presenting an hour long course on advanced accountancy on a small mobile screen may not be the greatest way to deliver this training. However, supplementing a desktop course with a short mobile course offering summary screens, takeaway guides and expert tip videos would be a great way of getting more mileage.

With the Adapt framework, courses can be easily tailored for different screen sizes, meaning you can customise the learning experience based on how your course is viewed, and all using the same source.

### Layout and Navigation

Perhaps the most immediately obvious difference between Adapt and other e-learning tools and frameworks is what’s possible with both layout and navigation; taking the lead from modern web design, scrolling pages are favoured over presenting information in a sequence of single, fixed-position pages.

These scrolling layouts provide us with:

- An opportunity to structure content in more varied ways.
- The ability to incorporate art direction throughout the course, rather than being limited to specific branding areas (such as the nav bar).
- No more need for unnecessary pages and extra navigation as a result of the designer running out of screen ‘real estate’.

### Learn your ABCs

<img src="https://github.com/adaptlearning/documentation/blob/master/04_wiki_assets/adapt_framework/adapt-a-b-c.jpg" alt="diagram illustrating the article, block, component hierarchy" align="right">

To better fit the new scrolling page design ethic, we've created a more suitable hierarchy and nomenclature inspired by print publications. Gone are the topics and screens of old; say hello to **pages**, **articles**, **blocks** and **components**!

**Pages** are how the main learning content is presented (similar to a page on the web), and can contain a number of sub-elements, making them perfect to present a single topic in an e-learning course.

**Articles** are the next step down, and are used to present compound pieces of information within the page. Like pages, articles can be formed of many sub-elements. Articles can also be used to split up a page for presentation purposes.

**Blocks** have replaced the traditional screens/slides found in most e-learning publishing software, and present small chunks of related content using **components**.

**Components** are the main interactions in Adapt, and present simple ideas. Components can be used in a block full-width, or combined with another component for more variety.

To summarise: **Pages** contain **Articles** contain **Blocks** contain **Components**.

Think **A**, **B**, **C**!

## Getting technical

The Adapt framework has been designed to be easily accessible to developers. By using popular web frameworks, and a modular plug-and-play architecture, you can spend more time developing fun stuff, and less time trying to integrate with the core product.

### Open standards and familiar frameworks

Rather than reinventing the wheel, the Adapt framework builds upon well established web standards and frameworks, meaning that most web developers coming to Adapt will already be familiar with some or all of the technologies we use:

- HTML/JavaScript/CSS with [LESS](http://lesscss.org/)
- [RequireJS](http://requirejs.org/) and [Backbone.js](http://backbonejs.org/) for structure
- [Handlebars](http://handlebarsjs.com/) for templating
- [Grunt](http://gruntjs.com/) for building and previewing
- JSON for course content and configuration

### Pluggable core

Adapt's core, while lightweight, has all the functionality you need to create complex plugins to enhance your courses. Our simple API encourages a modular style of coding and means that you can reuse your plugins in any of your Adapt courses.

Adapt plugins fit into four different categories:

**[Components](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#components)**: small interactive widgets (e.g. [text](https://github.com/adaptlearning/adapt-contrib-text), [slider](https://github.com/adaptlearning/adapt-contrib-slider)).<br>
**[Extensions](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#extensions)**: additional functionality extending the core (e.g. [resources](https://github.com/adaptlearning/adapt-contrib-resources), [assessment](https://github.com/adaptlearning/adapt-contrib-assessment)).<br>
**[Themes](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#themes)**: custom course styling (e.g. [vanilla](https://github.com/adaptlearning/adapt-contrib-vanilla)).<br>
**[Menus](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#menus)**: determines how the learner navigates through the course (e.g. [box menu](https://github.com/adaptlearning/adapt-contrib-boxmenu/)).

### Streamlined development and deployment with the Adapt command-line interface

Developed in tandem with the framework, the [Adapt command-line interface](https://github.com/adaptlearning/adapt_framework/wiki/Adapt-Command-Line-Interface) (CLI) is a set of tools aimed at simplifying the development of Adapt courses and plugins, by automating many of the Adapt workflows, such as creating new courses and creating, publishing and installing new plugins.

## Next steps

Now that you've had a run-down of the basics, you're ready to start experimenting on your own! Here are a few useful links to get started:

- [Setting up your development environment](https://github.com/adaptlearning/adapt_framework/wiki/Setting-up-your-development-environment)
- [Creating your first course](https://github.com/adaptlearning/adapt_framework/wiki/Creating-your-first-course)
- [Contributing to the Adapt framework](https://github.com/adaptlearning/adapt_framework/wiki/Contributing-to-the-Adapt-Framework)
- [Adapt learning community](https://community.adaptlearning.org/)
- [Frequently asked questions](https://github.com/adaptlearning/adapt_authoring/wiki/FAQ)