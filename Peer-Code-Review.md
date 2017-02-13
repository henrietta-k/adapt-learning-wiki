After writing some code (be it in the form of a new feature, or bug fix), it must go through a vetting process by the Adapt collaborators before it is incorporated in the collaborator-maintained codebases:

1. Code is submitted for review as a pull request.
2. Code is reviewed by peers with any discussion taking place in public, on the PR page itself.
3. Peers post their assessment of the code on the PR page and when they feel in the position to give a concrete verdict, give either a +1, +2 or -1 (reserved for exceptional circumstances).
4. Code is merged after the required +1s are received.

The process is governed by these rules:
* The developer who submits the PR is not allowed to cast a +1.
* If a commit is added to the PR, any +1s given so far are invalidated. Everyone must post their assessment/+1 after reviewing the commit.
* Any new functionality/feature requests uncovered during review of a PR must be separated into new issues/PRs.
* **For code to be merged, a minimum of three +1s is required. Of these, at least two +1s must have come from a core team member. All three +1s cannot come from reviewers working from the same company.**  
* The person who merges the PR must also post their +1 prior to merging if their vote is required.
* A vote of -1 must be accompanied by an explanation of why the PR should not be merged. Without this, the -1 will be disregarded.
* Any concerns signaled by a -1 warrant careful consideration, but no reviewer has veto rights. 
  1. Concerns will be resolved in conversation between the submitter of the PR and the reviewer who posted the -1. When/if satisfied, the reviewer will change the vote to +1.
  2. At an impasse, the Project Manager will specify a course of action.

### Review Scoring
Scores indicate the following:  
<dl>
<dt>-1: Do not commit.</dt>
<dd>A core developer may give a -1 because any (or all) of the following:<br /> 
- The code fails testing.<br />
- The code does not meet Adapt standards.<br />
- The code negatively impacts the application.<br />
- You have unresolved questions about the intent of the code.</dd>
<dt>+1: Commit.</dt>
<dd>A core developer may give a +1 because of the following:<br /> 
- You understand the intentions of the submitter.<br /> 
- You accept the implementation of the PR.<br />
- You don’t foresee any negative issues resulting from the proposed changes.
</dd>
<dt>+2: Commit.</dt>
<dd>In addition to the meaning of +1, a score of +2 indicates that you have tested the code and confirm it to be working. A vote of +2 does not count as two +1s.</dd>
</dl>

### Core Team Members

**Adapt Framework Core Developers:** Brian Quinn, Matt Leathes, Tom Taylor, Oliver Foster, Dan Gray, Thomas Berger, Tom Greenfield
 
**Adapt Authoring Tool Core Developers:** Dennis Heaney, Brian Quinn, Dan Gray, Tom Taylor, Thomas Berger

### References

[SmartBear: 11 Best Practices for Peer Code Review](http://smartbear.com/smartbear/media/pdfs/wp-cc-11-best-practices-of-peer-code-review.pdf)