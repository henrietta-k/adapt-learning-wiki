Accessibility settings/preferences are intended to help users with visual or motor impairments access Adapt courses.

## Landmarks in Adapt

### ARIA Landmark Roles

Landmarks help assistive technology users orient themselves to a page and help them navigate easily to various sections. Landmarks are attributes you can add to elements in your page to define areas like the main content or a navigation region.

We can define parts of a page using 'roles'. This allows screen reader users the ability to easily jump from one section to another and know where they are going.

Roles provide semantic information therefore these attributes should not be placed on elements that already have semantic meaning. They should only be placed on `<div>` and `<span>` elements. 

    <div class="menu-container" role="menu">
	<div class='menu-container-inner'>
		{{#if title}}
		<div class="menu-title">
			<h1 class="menu-title-inner">
				{{{title}}}
			</h1>
		</div>
		{{/if}}
		{{#if body}}
		<div class="menu-body">
			<div class="menu-body-inner">
				{{{body}}}
			</div>
		</div>
		{{/if}}
	</div>
    </div>


###Definition of Roles 

**alert** - A message with important, and usually time-sensitive, information.

**alertdialog** - A type of dialog that contains an alert message, where initial focus goes to an element within the dialog as with 'notify' pop-ups. 

**button** - An input that allows for user-triggered actions when clicked or pressed.

**checkbox** - A checkable input.

**complementary** - A supporting section of the document, designed to be complementary to the main content yet treated as a navigational landmark such as 'drawer'.

**dialog** - An application window that is designed to interrupt the current processing of an application in order to prompt the user to enter information or require a response such as 'tutor' extension.

**document** - Information that is declared as document content, as opposed to a web application. Used for media component transcript.

**heading** - A heading for a section of the page.

**link** - An interactive reference to an internal or external resource that, when activated, causes the user agent to navigate to that resource.

**main** - The main content of the page. There should only be one 'main' landmark per page.

**menu** - A type of widget that offers a list of choices to the user.

**menuitem** - An option in a set of choices contained by a menu or menubar.

**navigation** - Top bar collection of page navigation links. Standard consists of 'back button' 'progress bar' and 'drawer'.

**option** - A selectable item in a select list, such as 'matching' component.

**progressbar** - An element that displays the progress status for tasks that take a long time.

**radio** - A checkable input in a group of radio roles, only one of which can be checked at a time.

**search** - A search tool. Usually found in 'drawer'.

**slider** - A user input where the user selects a value from within a given range.

**textbox** - Input that allows free-form text as its value.



### Using ARIA Label in Adapt

The aria-label attribute is a description that is never displayed on screen but is relayed to a screen reader user. It defines a string that labels the current element. 

This attribute can be used with any typical HTML element; it is not limited to elements that have an ARIA role assigned. Use it in cases where a text label is not visible on the screen. 

  ` <div class="navigation-inner" role="navigation">
       <a href="#" class="navigation-back-button" aria-label="Back button"></a>
       <a href="#" class="navigation-drawer-toggle-button" aria-label="Drawer"></a>
   </div> `















 