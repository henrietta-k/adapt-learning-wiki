**Attendees**: Aniket, Brian, Dan Grey, Tom G, Matt, Ollie, Pete, Thomas B, Tom T.

**Time**: 11am Tuesday 6th December 2016.

## Framework v3

### Proposed changes
- Abandon IE8
- Abandon IE9
- Abandon IE10
- Refactor
	- Transition to ES6 (possibly using Typescript as a transpiler while support for IE11 persists)
	- Remove ‘sticking plaster’ fixes
- CLI rework (necessity if plugin architecture changed)
- Core audio support
- Multiple page rendering
- Unlink content structure: remove dependency on CO/A/B/C hierarchy
- iframe issue

### Actions
- List problems with current framework
- Architecture diagram **Ollie**
- Arrange extra-curricular discussions (around meetup? -- pub?)
- Look into iframe issue — moving navigation out of the wrapper **Ollie**

### Notes
- More user-led UI changes/user testing
	- Potentially develop analytics tracking (xAPI/google analytics)
	- User-input feedback/rating system
- Look into creating handouts/community pack to hand out at the meetup (particularly from a non-technical perspective)
	- Call to action
	- Generating feedback
- Aniket has a UX group based in India with around 250 members who could potentially review UI/UX
- Properly adopt semantic versioning
	- Will likely cause issues with plugin dependencies