## Purpose of this document:
To define the requirements and approach for RTL support in Adapt RTL framework. This should be used as a basis for content builders who plan to develop RTL courses, and for developers who work on core and contributed extensions that should support RTL directionality.

## Functional Requirements list:
**1. Ability to determine course default direction should affect all course elements:**
* Ideally a single setting would trickle down to all course elements, components, extensions, etc.
* Default direction would be set as LTR
* Allow and define how contributed components and extensions can support RTL, as long as the extensions conform to the Adapt RTL guidelines

**2. Display text in correct RTL format, including:**
* Signs such as full stop, exclamation mark, question mark, etc. appear in their correct location in the sentence and do not break sentence structure
* When using RTL, Latin text within an RTL sentence appears in correct location in the sentence and does not break sentence structure
* Text typing in interactive elements such as text boxes and essay answer boxes functions in proper RTL 

**3. Where relevant, choosing RTL would change the directionality of images and icons appropriate for RTL - e.g. arrows, progress bars, icons, etc.**

**4. Support RTL position and directionality of page and component layout and movement, for example:**
* HTML text including lists, tables, etc. appear as RTL
* Correct rendering of page elements to support reading from right to left
* Progress of multi-part and interactive elements (e.g. narrative) is moving from right to left
* Animation and easing directionality is adjusted for RTL behavior (e.g. opening of drawer, menus)

**5. Maintain the separation of content and design and handle directionality via components style and javascript and not via course content (i.e. no need to use 
`<p style="direction: rtl;"> `
inside the course content, but rather define the RTL at course settings level)**

## Coding approach guidelines:
**1. Use `.dir-rtl &` to append RTL style changes in LESS files of theme/component**
**2. Most CSS/LESS RTL adjustments normally have to do with:**
* Direction - rtl - to be handled at Body element level
* Align text left/right
* Float elements right/left
* Left/right margin/padding
* Relative and absolute positions of elements
* Shadows that have left/right properties
* Choice of correct icons and images (e.g. arrows, progress bars)
**3. Use variables and if statements in javascript to calculate correct RTL direction, position and movement, etc.**
