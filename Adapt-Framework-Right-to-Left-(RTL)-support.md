We've created this page to define the requirements and approach for RTL support in the Adapt framework, and help developers who wish to support such functionality in their own courses. The good news is that by default, the framework and all of the core plugins are RTL-compatible, and supported by the core team.

However, there are a number of things you will need to do as a developer to make sure that your content looks its best for RTL users.

## Functional Requirements:

The following points summarise what we, as Adapt developers aim to deliver for RTL users.

**1. Ability to determine course default direction**
* LTR is the default text direction.
* Text direction trickles down to all course elements from a single `config.json` setting.

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

**4. Activate RTL by adding/changing the default Direction setting "_defaultDirection": "rtl", in src/course/config.json.**

## Useful Links
- [Moodle CSS Coding Style: RTL](https://docs.moodle.org/dev/CSS_coding_style#Right-to-left)
- [Readying Your Site For RTL](http://tech.pro/tutorial/1738/readying-your-site-for-rtl)
- [The Guide to create RTL adaptations of LTR CSS](http://www.numediaweb.com/guide-create-rtl-adaptations-css/927)