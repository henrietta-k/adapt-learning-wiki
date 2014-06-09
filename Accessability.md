# Landmarks in Adapt

### Landmark Roles

Landmarks are attributes you can add to elements in your page to define areas like the main content or a navigation region.

We can define parts of a page using roles. This allows screen reader users the ability to easily jump from one section to another and know where they are going.
 

**navigation** - Top bar collection of page navigation links. Standard consists of 'back button' 'progress bar' and 'drawer'.

`<div class="navigation-inner clearfix" role="navigation">`

**main** - The main content of the page. There should only be one 'main' landmark per page.

**dialog** - Feedback, often in pop-up form such as tutor extension.

`<div class="notify-popup notify-type-{{_type}}" role="dialog">`

**search** - A search tool. Usually found in drawer.

**button** - An input that allows for user-triggered actions when clicked or pressed.

**checkbox** - A checkable input.

**heading** - A heading for a section of the page.

**menu** - A type of widget that offers a list of choices to the user.

**menuitem** - An option in a set of choices contained by a menu or menubar.

**progressbar** - An element that displays the progress status for tasks that take a long time.

**radio** - A checkable input in a group of radio roles, only one of which can be checked at a time.

**slider** - A user input where the user selects a value from within a given range.

**textbox** - Input that allows free-form text as its value.








 