_**Note:** This article assumes that you understand the [basic concepts of the git version control system](https://help.github.com/articles/good-resources-for-learning-git-and-github/)._

### Overview

On the Adapt project, our mantra when it comes to releasing new versions of the framework and core plugins is 'little and often'. To achieve this, we've adopted a similar cut-down approach to the popular 'git flow' model to that [used by GitHub](https://guides.github.com/introduction/flow/): we've done away with develop branches in favour of merging directly into master, which not only means much less testing is required, but more importantly for our users, much more frequent releases :tada: (something which we find works much better with the oft fluctuating developer resource we rely on).

On the Adapt project, we organise the branches in our repos according to GitHub flow - a simplified variation of the git flow model. For those familiar with git flow, you will notice that there are no develop branches anywhere to be found ***(you can read more about GitHub flow [here](https://guides.github.com/introduction/flow/))***.

### Branching

We use the following branches in the core Adapt repositories:

Name | Description | Persisting
---- | ----------- | ----------
`master` | Contains the stable, released code. | yes
`release/VERSION_NAME`<br/>*(e.g. `release/v2.0`)* | A release candidate branch. Contains **development** code, and should not be considered stable. Use this code at your own risk! | no
`issue/TICKET_NAME` <br/>*(e.g. `issue/1024`)* | A self-contained bug-fix. Should be named after a corresponding issue ID. Finished changes should be submitted as a pull request. | no
`feature/FEATURE_NAME` | A self-contained feature. This should also be named with an issue ID (see above). Finished changes should be submitted as a pull request. | no

We also apply the following rules to the core Adapt repos (i.e. those owned by [@adaptlearning](https://github.com/adaptlearning)):

* The `master` branch is the only persisting branch. All other branches should be deleted post-merge.
* Core Adapt repos should only ever have `master` and `release` branches.
* The `master` branch contains only *thoroughly* tested code, and should only ever merge code from a `release` branch.
* `feature` branches represent isolated, new functionality, and should be taken from the latest `release` branch. Once work is complete, code should be submitted as a pull request (PR) to the latest `release` branch (**NOT** `master`).
* Bug fixes (i.e. `issue` branches) should be submitted as a PR to the current `release` branch (**NOT** `master` -- due to our frequent release schedule, we don't allow hotfixes directly into `master`).
* Anyone who is making a change to a repo should create and work from their own fork (including where possible, the core team).

### Gearing up for release

We go through the following schedule prior to making a release:

1. The core development team assign a bunch of issues/features to the relevant release in our [bug tracker](https://github.com/adaptlearning/adapt_framework/wiki/Using-the-bug-tracker).
1. A `release` branch is created from the latest `master` code.
1. The coders are let loose :wrench:, and submit their additions as PRs using the aforementioned process.
1. Once all work has been done, we call a code freeze :snowflake:, and the branch goes through our testing process.
1. Any issues found during testing are fixed.
1. Once the testing team are happy, we're good to release.

### Releasing

Once the release code has been properly tested, we are ready to merge back into master. When this is done, we tag the master branch with the release number, and **party**! :tada::balloon::tropical_drink: