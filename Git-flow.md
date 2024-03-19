### This document outlines the git process used for the framework product. For information on the authoring tool's process, see [this page](https://github.com/adaptlearning/adapt_authoring/wiki/Git-process).

_**Note:** This article assumes that you understand the [basic concepts of the git version control system](https://help.github.com/articles/good-resources-for-learning-git-and-github/)._

### Overview

On the Adapt project, our mantra when it comes to releasing new versions of the framework and core plugins is 'little and often'. To achieve this, we've adopted a similar cut-down approach to the popular 'git flow' model to that is [used by GitHub](https://guides.github.com/introduction/flow/): we've done away with develop branches in favour of merging directly into master, which not only means much less testing is required, but more importantly for our users, much more frequent releases :tada: (something which we find works much better with the oft fluctuating developer resource we rely on).

On the Adapt project, we organise the branches in our repos according to GitHub flow - a simplified variation of the git flow model. For those familiar with git flow, you will notice that there are no develop branches anywhere to be found ***(you can read more about GitHub flow [here](https://guides.github.com/introduction/flow/))***.

## Purpose
In order to control rework and therefore production costs, especially around bug resolution, it is extremely important that we work collaboratively around the central [Adapt Learning code repositories](https://github.com/adaptlearning/) on [GitHub](https://en.wikipedia.org/wiki/GitHub).<br/><br/>
This document will outline the [git](https://en.wikipedia.org/wiki/Git) workflow and some basic commands and techniques you can use, with the express intention of improving your collaborative programming skills.<br/>

## Context
There are three major types of programming task for Adapt programmers; custom work, bug fixing and feature creation. We use GitHub to store the common codebase. GitHub is where bug fixing work should occur and where reusable behaviour is kept as plugins, this enables us to carry existing solutions into future projects in an organised and documented manner.<br/>

## Prerequisites
The [git command line interface](https://git-scm.com/downloads) should be installed, preferably with a Unix-style terminal. It is possible to use the Windows Command Line (the windows version of a terminal) directly, however file paths and binary execution differ significantly between native Windows and Unix-style terminals. A Unix-style terminal is more commonplace in the wider web development community, this is as native versions of the Unix terminal are included with macOS and all Linux-type operating systems, these systems are used heavily in the web-design and web-server communities.
It is advisable to create a directory in the root of your hard drive or user folder (c:\working\adapt) for downloading source code for editing.<br/>

## Current situation
For the Adapt Learning open-source repositories, the Adapt community runs its Adapt Framework workload from a [Kanban project board](https://github.com/orgs/adaptlearning/projects/2). The Kanban project board allows us to triage and assign issues (bug reports, feature requests, etc) and also to publish and review codebase changes to those issues as pull requests.<br/>

## Kanban management
[New issues](https://github.com/adaptlearning/adapt-contrib-core/issues) are attached to the board in the ‘new’ column, from each of the repos in the Adapt Learning organisation, automated by [Git Actions](https://github.com/adaptlearning/adapt_framework/actions/workflows/addtomainproject.yml) on each repository.<br/><br/>
Each issue is [labelled](https://github.com/adaptlearning/adapt-contrib-core/labels) as a ‘bug’, ‘enhancement’ or ‘breaking’ change which aligns it to the [semver](https://docs.npmjs.com/about-semantic-versioning) versioning segments from revision to major.<br/><br/>
When an issue is assigned to a person or people, the issue should be moved to the ‘assigned’ column on the Kanban board and the relevant accounts should be assigned to the issue using the GitHub user interface.<br/><br/>
[A branch is created](https://github.com/adaptlearning/adapt-contrib-core/branches) on the relevant repository, or a fork of the repository, according to its issue number (issue/245, issue/3491, etc). <br/><br/>
When code is pushed into the newly created issue branch and the branch is ready for review, a pull request should be created for the branch, requesting for the branch to be merged into the Adapt Learning repository’s master branch. The pull request title should be in the format “Type: Short description (fixes #123)”, the type should be either Fix, Update, New, or Breaking as this will initiate an automated version bump and an automated release once the pr is merged. If a version bump isn't required, for example README updates or formatting amends, then the type should be Chore. The pull request comment should connect the pull request to the original issue (fixes #245, fixes #3491, etc) and the pull request comment should explain how the pull request fixes the issue. Both the pull request and the issue should be placed into the ‘needs reviewing’ column on the Kanban board.<br/><br/>
When two contributors and any other person have accepted the changes and once all comments and suggestions have been resolved, the pull request can be ‘squash merged’ into the master repository, the title of the squash-merge should follow the “Type: Short Description (fixes #123)” convention as it is this message that determines the automated release. Before merging the pull request, it may be necessary to bump the package.json framework version number to ensure that the plugin requests the correct core code, if any version specific behaviour is required. <br/>
After merging the pull request it will become closed and should close any associated issue, both the issue and the pull request will be automatically moved to the ‘needs releasing’ column where a GitHub Action will bump the package.json version number according to the types of commits in the release, it will duplicate the package.json into the bower.json, create a new repository release with a change log and add the label ‘released’ to the issue and pull request.<br/>


### Branching

We use the following branches in the core Adapt repositories:

Name | Description | Persisting
---- | ----------- | ----------
`master` | Contains the stable, released code. | yes
`issue/TICKET_NAME` <br/>*(e.g. `issue/1024`)* | A self-contained bug-fix. Should be named after a corresponding issue ID. Finished changes should be submitted as a pull request. | no

We also apply the following rules to the core Adapt repos (i.e. those owned by [@adaptlearning](https://github.com/adaptlearning)):

* The `master` branch is the only persisting branch. All other branches should be deleted post-merge.
* The `master` branch contains only *thoroughly* tested code.
* Bug fixes (i.e. `issue` branches) should be submitted as a PR to the `master` branch.

## Git projects
A git project is a folder on your hard drive which keeps a journal of file change commits, in branches, to which you can commit, pull, merge and push other file change commits.<br/><br/>
Each git project can have ‘remotes’, which are external repositories with branches from which you can pull or push commit histories.
You can use the git command line client (recommended), or the git user interface and some SVN clients to manage a git project, pushing and pulling local changes to and from remotes as required.<br/>

## Git terminal commands

### Create a new plugin
[Create a new repository](https://github.com/organizations/adaptlearning/repositories/new) on github.com and in a new local project folder, run the following commands from a terminal:

#### Turn the current folder into a git project
`$ git init`

#### Add a remote to your project, called ‘origin’, pointing to the new repository URL
`$ git remote add origin https://github.com/adaptlearning/adapt-contrib-name`

#### Add all of the available files to the commit
`$ git add -A *`

#### Commit the changes, adding a commit message
`$ git commit -m "Initial commit"`

#### Push the commits to the remote master branch
`$ git push origin master`<br/><br/>
Note: Remember to .gitignore the node_modules if necessary

### Download an existing repository to a git project

#### To create a local project from an existing repository in an existing folder
`$ git clone https://github.com/adaptlearning/adapt-contrib-name .`

#### To create a local project from an existing repository in a new folder
`$ git clone https://github.com/adaptlearning/adapt-contrib-name folderName`

### Commit changes to an existing git project and push to a remote repository branch

#### Create a new branch
`$ git checkout -b issue/786`

#### Check the status of the files against the current branch
`$ git status`

#### Remove a file
`$ git rm path/filename.ext`

#### Remove a folder
`$ git rm -rf path/`

#### Revert a path
`$ git checkout path/`

#### View the differences against the current branch in the vim file editor
`$ git diff`<br/><br/>
Note: Use the command :q or ctrl+c to leave vim. Use space to view the next page of diffs.

#### Add all available files to the commit
`$ git add -A *`

#### Add a single file or folder to the commit
`$ git add path/filename.ext`

#### Commit the changes, adding a commit message
`$ git commit -m "Fix: Comment about the fix (fixes #786)”`

#### Push branch commits to the origin repository
`$ git push origin issue/786`

## Comparing changes over time
A history of issues, pull requests and commits is built up over time for each plugin. As such, it is possible to compare versions directly on GitHub, to see the change logs over time, to compare branch versions directly in a git project and to ascertain whether a bugfix should be ported into an ongoing Adapt project. It is possible to be very accurate and specific as a result of the ongoing version control mechanisms supported by git projects and the GitHub website.<br/><br/>
It is also possible to compare two versions of a git project folder, two plugins, or two courses for file changes using a file differencing and merging tool by simply comparing their folders. [Winmerge](https://winmerge.org/) and [meld](https://meldmerge.org/) are two good examples of diffing tools.

## Create, editing and testing plugins
It is generally best to edit plugins inside an Adapt Framework project folder. This is as the adapt_framework repository provides a central place for code standardisation, as well as the adapt build tools for easy testing.

### Create a test course

#### Clone the adapt framework into an issue specific project folder
`$ git clone https://github.com/adaptlearning/adapt_framework 123-core-issue-description`

#### Enter the folder
`$ cd 123-core-issue-description`

#### Download the core, install the dependencies and download the plugins as git projects
`$ npm install && adapt devinstall`<br/><br/>
It should be possible to create, edit, commit and review plugins from this folder. You can checkout branches in of a specific plugin or the core to review code from the community.

#### Checkout an existing branch for testing
`$ git checkout issue/123`

#### Build the project with source mapping enabled
`$ grunt dev`