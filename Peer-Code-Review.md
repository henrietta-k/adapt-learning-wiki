After writing some code (be it in the form of a new feature, or bug fix), it must go through a vetting process by the Adapt collaborators before it is incorporated in the collaborator-maintained codebases:

1. Code is submitted for review as a pull request.
1. Code is then reviewed by peers using GitHub's [pull-request review](https://help.github.com/articles/about-pull-request-reviews/) feature to leave comments where necessary and give an approval/rejection.
1. Code is amended if needed until it satisfies the required number of approvals.
1. Provided all unit tests are passing, code is merged.

The process is governed by these rules:
* The developer who submits the PR is not allowed to submit a review.
* If a commit is added to the PR, any previously given reviews are invalidated. Everyone must re-post their verdicts after reviewing the commit.
* Any new functionality/feature requests uncovered during review of a PR must be separated into new issues/PRs, unless directly related.
* **For code to be merged, a minimum of three approvals is required. Of these, at least two must have come from a core team member. In the interest of impartiality, it is generally not advised to get all three approvals from a single collaborating company.**  
* The person who merges the PR must also submit their review prior to merging **if their vote is required**. Merging a PR which already has enough approvals does not require the review of the merger themselves.
* Any review rejections must be accompanied by an adequate explanation of why the PR should not be merged. Without this, the review will be disregarded.
* Any concerns signalled by a 'rejected' review warrant careful consideration, but no reviewer has veto rights. If the PR receives enough approvals, it can still be merged (provided the other rules outlined on this page are followed).
  1. Concerns will be resolved in conversation between the submitter of the PR and the reviewer who rejected the PR. When/if satisfied, the reviewer will change verdict to an approval.
  2. At an impasse, a course of action will be decided by the core development team.

### Review Scoring
Scores indicate the following:  
<dl>
<dt>Request changes.</dt>
<dd>A core developer may reject a PR because any (or all) of the following:<br /> 
- The code fails testing.<br />
- The code does not meet Adapt standards.<br />
- The code negatively impacts the application.<br />
- You have unresolved questions about the intent of the code.</dd>
<dt>Approved.</dt>
<dd>A core developer will approve an PR because of the following:<br /> 
- You understand the intentions of the submitter.<br /> 
- You accept the implementation of the PR.<br />
- The submitted code complies with the code-style outlined in the project's [styleguide](https://github.com/adaptlearning/documentation/blob/master/01_cross_workstream/style_guide.md).
- The code passes all automated tests.
- You don’t foresee any negative issues resulting from the proposed changes.
</dd>
</dl>

### Core Team Members

**Adapt Framework Core Developers:** Thomas Berger, Oliver Foster, Dan Gray, Tom Greenfield, Matt Leathes, Brian Quinn, Tom Taylor
 
**Adapt Authoring Tool Core Developers:** Thomas Berger, Dan Gray, Tom Greenfield, Dennis Heaney, Brian Quinn, Tom Taylor

### References

[SmartBear: 11 Best Practices for Peer Code Review](http://smartbear.com/smartbear/media/pdfs/wp-cc-11-best-practices-of-peer-code-review.pdf)