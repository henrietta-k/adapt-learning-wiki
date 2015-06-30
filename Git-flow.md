_**Note:** This article assumes that you understand the [basic concepts of the git version control system](https://help.github.com/articles/good-resources-for-learning-git-and-github/)._

On the Adapt project, we've adopted the git flow model to organise our repos using branches (which you can read more about in [this article](http://nvie.com/posts/a-successful-git-branching-model/)). This process may be too involved for smaller plugins, but as a rule, it's important to always separate your release code from your in-development code (i.e. master and develop).

We use the following branches:

Name | Description | Persisting
---- | ----------- | ----------
`master` | Contains the stable, released code. | yes
`develop` | The ‘working’ branch. Is the the parent of all feature and release branches, and contains the latest code. Develop **does not** contain tested code, and should definitely not be considered production ready. | yes
`release/VERSION_NAME` | (e.g. `release/v2.0`)<br> A release candidate branch. Contains code currently being tested. | no
`hotfix/TICKET_NAME` | (e.g. `hotfix/ABU-001`)<br> Self-contained bug-fix. Should not be pushed to the core repo, but rather a personal fork. Changes submitted as a pull request | no
`feature/FEATURE_NAME` | This is also likely to be named after a JIRA ticket (see above).<br> Self-contained feature. Should not be pushed to the core repo, but rather a personal fork. Changes submitted as a pull request | no

We apply the following rules to the core Adapt repos (i.e. those owned by [@adaptlearning](https://github.com/adaptlearning)):

* Core repos should only ever have `master`, `develop`, and `release` branches.
* The `master` branch contains only thoroughly tested code, and only ever merges in `release` branches (and `hotfix` branches in the case that an urgent bug is found).
* Feature branches represent isolated, new functionality, and should be taken from develop.
* Hotfix branches are used to fix issues, and merged into both `develop` and `master`.
* The `master` and `develop` branches are the only persisting branches. All other branches should be deleted post-merge.
* Anyone who is making a change to a repo creates their own fork, and works from that (this should include the core team). 
* PRs work in the same way.

### Gearing up for release

When a release is planned, we create a release branch from `develop` at the point that represents the required feature set. Once this release branch is created, only fixes are made to it, no further additions. After this branch has been thoroughly tested, and any bugs fixed, it is merged with `master` (and optionally `develop`, to make sure that all fixes have been carried across) and deleted. A 'tag' is added to the master branch to signify the new release.