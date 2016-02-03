We use GitHub's [issues](https://guides.github.com/features/issues/) feature to track our ever-longer **TODO** list for the Adapt project. This includes bugs, new features, discussion points, and anything else code-related that needs attention. In an attempt to make everyone's lives easier, we've only turned on the issues for the **adapt_framework** repository, and use labels to filter the different areas. 

## Exploring the backlog

As you'll soon find out, we have a healthy collection of bugs and feature requests in our pot. To make browsing these as painless as possible, we try to add useful labels such as *accessibility* to make filtering a bit easier.

## Reporting issues

Read on for a checklist of *do*s and *don't*s regarding logging issues.

### Bugs

<img src="https://github.com/taylortom/notes/blob/master/assets/bug-feature.jpg" align="right">
If you think you’ve found a bug, there are a few things to consider before logging a new issue:

**Can you replicate it?** If the answer to this is no, please think carefully before logging an issue. Although we take bugs seriously, our development time is limited and we can’t afford to spend it failing to replicate bugs.

**Has the issue been reported before?** We have already built up a sizeable back-log of issues, so the issue may have been reported by someone already. Please do therefore [search the list of issues](https://adaptlearning.atlassian.net/issues/) first. If it has already been reported, any extra information you have garnered from your own tests could be invaluable in fixing it, so please add any such info to the existing ticket, should you find one.

**Is it covered?** By this we mean: is your set-up listed in the [v2.0.0 standards definitions document](https://community.adaptlearning.org/pluginfile.php/24/mod_forum/attachment/3397/Adapt_Framework_v2.0.0_standards_definitions_draft.pdf)? In an ideal world, we’d commit to supporting Adapt on all browsers and operating systems. Unfortunately this isn’t feasible with the resources we have, so we have to prioritise those named in the standards definition.

#### What to report

If your bug passes the above tests, the next step is to create an issue.

Try to give your issue a succinct name. Something short, but which still give the reader a good summary of the problem without needing to open the issue. Also try to reference the plugin name (if applicable) - leave out the `adapt-contrib` prefix where possible to cut down on characters :smile:

The main body of the issue needs to contain as much detail as possible about the bug you can provide. This should focus on the following:

A **description** of the bug, **steps** on how to replicate it and your **set up** (i.e. browser and operating system - [aboutmybrowser](http://aboutmybrowser.com) can be useful here). Feel free to include any other information which you think may be useful, screenshots in particular can often give more useful information than words alone!

Make a note of any JavaScript errors you see. You may need to press F12 to reveal your browser's developer tools. If you are testing using a tablet or smartphone you will need to connect it to your PC or Mac in order to get access to the developer tools.

If your bug depends upon certain configuration options in order to be replicable, it is vital that you state these (or copy the require JSON into the issue and mark as a codeblock - GitHub issues support [markdown](https://guides.github.com/features/mastering-markdown/)).

### Features

If there's a feature you'd like to see in Adapt, we'd love to hear from you!

We manage feature requests in the same way as issues, so much of [the above](#reporting-an-issue) applies. **The most important thing to remember** when requesting a new feature, is to add `feature-request` to the **Labels** field (you might also want to give a more appropriate **Issue type** than *Bug*!).

Try to give as much detail about your request as you can in the description, as this will give us the best idea of what you want. It would also be beneficial to leave you GitHub username, so we can get in touch with you if we implement your feature.

*A few of the fields mentioned above won't be applicable to feature requests, so feel free to leave those blank.*

## Working on issues

We are always grateful for any time you have to contribute to the Adapt project. Depending on your experience level and confidence, there are a number of ways you can begin contributing.

#### Bugs

Fixing bugs is a great way to dip your toe into the warm Adapt waters. Head to our [bug tracker](https://github.com/adaptlearning/adapt_framework/wiki/Using-the-bug-tracker) and look for issues with the **good-first-bug** or **mentored-bug** labels for some more straighforward tasks. The former should be accessible to developers of any experience level, while the latter may require some more metaphorical hand-holding from one of the core development team.

#### New features

If you're confident working with the framework on a larger scale, why not grab a [feature-request](https://github.com/adaptlearning/adapt_framework/issues?q=is%3Aopen+is%3Aissue+label%3A%22feature+request%22) issue and give that a go? 

Regardless of the feature, there will probably be some discussion amongst the community/core team needed before you can get knee-deep in code. It's a good idea therefore to head to [Gitter](https://gitter.im/orgs/adaptlearning/rooms) to get the ball rolling and give everyone a heads-up on what you're thinking of doing so we can advise you on the best route to take. Also be sure to have a look at our [guide to contributing code](https://github.com/adaptlearning/adapt_framework/wiki/Contributing-code), which has some handy tips!

***

If you have any questions which haven't been answered here, please have a look through the [official GitHub issue documentation](https://guides.github.com/features/issues/), or ask the community in one of our [Gitter rooms](https://gitter.im/orgs/adaptlearning/rooms).