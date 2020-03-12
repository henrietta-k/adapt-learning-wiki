**In this document, we assume a basic working knowledge of Adapt. If you're completely new, we recommend you first check out the [Framework in five minutes](https://github.com/adaptlearning/adapt_framework/wiki/Framework-in-five-minutes), then try [creating your own course](https://github.com/adaptlearning/adapt_framework/wiki/Creating-your-first-course) to learn the ropes.**

## What skills do I need?

The technology stack used in the Adapt framework is intended to be accessible to new developers. As such, you should recognise some, or all of the technologies/frameworks that Adapt uses. See below for a brief breakdown, as well as links to useful related resources:

### Required

**JavaScript and HTML**: This really goes without saying as Adapt courses are web-apps, but it is essential that you're comfortable working with JavaScript and HTML.

**Backbone**: In addition to giving the code an organised MV* structure, Backbone also adds a few nice bells and whistles such as a [page routing system](http://backbonejs.org/#Router), and a very versatile [events module](http://backbonejs.org/#Events).

**Handlebars**: Our templating engine of choice, Handlebars is used for all of the front-end HTML for Adapt, from the plugins, to the core elements such as the nav bar.

**CSS**: We use LESS-preprocessed CSS for the styling of all elements in Adapt, so it's vital to at least have an understanding of the basics.

### Beneficial

The following are supporting libraries and frameworks; not essential to know, but very useful nonetheless.

**Jquery & Underscore**: If you've done any web development in the last 10 years, chances are you've probably worked with either (or both) of these utility libraries. With everything from type checking, to looping, to animation, these two libraries are very useful strings to have in your Adapt bow.

**Grunt (node)**: we use grunt to automate the building of the courses (code compilation/minification, asset management, JSON validation). If this is something that interests you, we recommend looking up the Grunt documentation, and learning a little Node.js.

## Finding something to work on

The first step contributing code to the project is to find an area that you want to work on - something that can be easier said than done.

If you already have something in mind - maybe you've found a bug, or there's a specific plugin you want to develop, great! Otherwise, we've written [a few tips](https://github.com/adaptlearning/adapt_framework/wiki/Bugs-and-features/) on our Bugs and features page on how you can get started.

### Shout about it!

Whatever you're working on, head to our [Gitter rooms](https://gitter.im/orgs/adaptlearning/rooms) if you need any help - we're a friendly bunch, and love to help!

## Working with Adapt

We've tried to make installing and running Adapt as painless as possible by providing the [command line tool](https://github.com/adaptlearning/adapt_framework/wiki/Adapt-Command-Line-Interface), which automates a lot of the more tedious tasks.

### Installing

Before working on Adapt, you'll need to [do a few things](https://github.com/adaptlearning/adapt_framework/wiki/Setting-up-your-development-environment) to make sure you've got all of the required tools and libraries.

Adapt requires few pre-requisites prior so if you haven't already, get up-and-running with Adapt by following the [install guide](https://github.com/adaptlearning/adapt_framework/wiki/Manual-installation-of-the-Adapt-framework).

## Submitting your code

Ok, so you've already gotten yourself acquainted with the code, and have something to contribute back. The next step is to show us what you've done!

We use GitHub's pull request (PR) model to merge changes into the framework. For those unfamiliar with this, head over to [this section](https://help.github.com/articles/proposing-changes-to-a-project-with-pull-requests/) in GitHub's help archives for a good selection of articles on the topic.

### Reason for PR'ing

You don't necessarily have to submit *complete* code when you create a PR for us to look at. The following are all valid reasons to open one:

- You have a bug fix
- You've implemented a new feature
- You've started fixing a bug/implementing a new feature, but are unsure how to continue
- You've started fixing a bug/implementing a new feature, but don't have time to contribute further

If your work is unfinished, don't worry. Pull requests are a great way to start a discussion and show the core team what you're working on, as well as get some advice on implementation *before* you've finished coding, saving you time in the long-run.

### Before submitting

Before you submit a PR to us, there are a few hoops that we ask you to jump through in the interest of transparency:

- **Does your code work?** This may seem obvious, but if we can't test your code, it's not going to be merged. Please make sure that anything you submit actually works :smile:
- **Does your code have a related Github issue?** It's important that we keep a paper-trail regarding work done on the project; this helps us to keep a track of what's going on, and allows us to plan and manage our available developer resource effectively. Please make sure that there's an accompanying Github issue to go with your PR, be it a bug fix, new feature, or anything else (see our [page on reporting bugs](https://github.com/adaptlearning/adapt_framework/wiki/Bugs-and-features#reporting-bugs) for more information on this).
- **Does your code comply to the Adapt code styleguide?** To give everyone working on the project an easier ride, we like to keep the coding style consistent across the breadth of Adapt repositories. Please make sure yours also complies to [our standards](https://github.com/adaptlearning/documentation/blob/master/01_cross_workstream/style_guide.md).
- **Have you updated the documentation and/or properties.schema?** If your change involves adding a new property to - or changing an existing property in - the JSON then that change will likely need to be reflected in the documentation (README.md, example.json) and properties.schema

### Creating a good PR
Remember that the purpose of the pull request is to allow the other contributors to review what you have written. To this end, it's important that you have:
* included a reference to the related GitHub issue/feature request (ideally using [the keyword technique](https://help.github.com/en/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword))
* commented your commits well
* given a short overview of what you've done
* described the expected behaviour after the changes
* listed any steps that need to be taken to check the changes
* noted anything that should be ignored (e.g. a known issue that you are not addressing)
* included screenshots if necessary
There's a good [guide to commit messages and PRs](http://www.sitepoint.com/how-good-are-your-html-and-css-comments/) (you'll have to scroll down a bit) by [Georgie Luhur](http://www.sitepoint.com/author/gluhur/) over at sitepoint that's worth a read - it also has some great tips on commenting your code well.

### Peer code review

After you have submitted your code, it will undergo a peer review process carried out by the core development team. You can read more about this here:

[Adapt peer code review process](https://github.com/adaptlearning/adapt_framework/wiki/Peer-Code-Review).

### Merging

When your code passes our peer review process, it's good to go! A member of the core team should be along shortly to merge the code. If this doesn't happen, feel free to give the team a gentle nudge in the [framework Gitter room](https://gitter.im/adaptlearning/adapt_framework).

## Repeat!

If you've gotten this far, congratulations! :tada: You're now a contributing member of the Adapt project! We greatly appreciate any time you can give to the project, however small you think it may be :smile:
