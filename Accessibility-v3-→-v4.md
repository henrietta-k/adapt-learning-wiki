## What has changed?
Adapt Framework v2 and v3 have an 'accessibility mode' which, when enabled through a button at the start of the course (accessible only via a <kbd>tab</kbd> keypress in v2), causes virtually all elements on the page to be 'tabbable'.

While the tabbing approach worked well and was popular with casual users of screen readers, we received feedback that it wasn't the best way to implement accessibility. Blind users universally reported that the Adapt accessibility implementation confounded their expectations of how they should navigate through the content with a screen reader (as standard keyboard shortcuts were not supported in the v2/3 implementation), and these users rejected the approach of having a specific accessibility 'mode'. Accessibility specialists from organisations who use Adapt agreed, and additionally pointed out that the tabbed approach did not align with the WCAG guidelines.

In Adapt v4, the framework's accessibility implementation has been re-engineered to follow WCAG guidelines. This change effectively reverts tabbing to default browser behaviour (interactive elements only) and removes the need for an 'accessibility mode'.

## Prerequisite understandings
### Standards
[W3C Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/about/) being a sub-group of [World Wide Web Consortium (W3C)](https://www.w3.org/Consortium/) produce the [guidelines and standards](https://www.w3.org/WAI/standards-guidelines/) for web accessibility. Out of these guidelines, the [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/#intro) are the most relevant to the Adapt Framework and content produced using it.

### What is accessibility?
Accessibility is often seen as an additional and restrictive set of design patterns catering for only people with recognised disabilities. The reality is much more subtle and much broader in scope. Some essential reading can be found at [W3C WAI - Accessibility Fundamentals - Introduction to Web Accessibility](https://www.w3.org/WAI/fundamentals/accessibility-intro/) and [Mozilla - MDN - Handling common accessibility problems](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility).

### Scope of accessibility in Adapt Framework
As developers of the framework, we have no control over the plugins, assets, content or styling included in a final course. The scope of accessibility within Adapt is naturally, therefore, limited to ensuring that the Framework gives the course author the ability to create a course that is accessible. The Framework cannot do this for the author - nor can it ensure that the author has done so - as what constitutes 'accessible' is subjective and will naturally vary from course to course. 

The onus is therefore on the course author to:
* understand what exactly 'accessible' means for learners with accessibility requirements
* configure the course correctly to enable that level of accessibility
* ensure that only plugins, assets & content that meet that level of accessibility are used in the course
* verify through testing that the course has been successfully configured and meets the learners' requirements as best as possible

The bulk of the accessibility work in the Adapt Framework - if we necessarily exclude content - revolves around screen reader access as ensuring that the framework efficiently describes visual content to users who are not able to see it is the biggest challenge to creating accessible online content. This document will mostly cover how we facilitate screen reader access with references for further reading.

**Note:** All of the specifications and recommendations utilised in the Adapt Framework are tested as working. Anything which cannot provide a consistent experience (whilst excusing minor variations) across the most commonly used screen readers and browsers should not be utilised in the framework.

### Screen readers and the browser
A standard browser 'tabbing cursor' follows the tabbability of elements through the DOM order. Tabbability is determined and reordered by the (implied or explicitly declared) value of each element's [tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) attribute. 

Elements gain and lose 'focus' as the learner navigates through the page, with the currently focused tabbable element being represented by the [`document.activeElement`](https://developer.mozilla.org/en-US/docs/Web/API/DocumentOrShadowRoot/activeElement) value. 

Focus, which determines the position of the tabbing cursor, can be moved through the document with the <kbd>tab</kbd> key (forward), the <kbd>shift</kbd>+<kbd>tab</kbd> keys (backward) and by clicking or tapping on various tabbable elements.

A screen reader adds a distinct second cursor to the browser: the 'screen reader cursor'. The screen reader cursor follows the readability of elements through the DOM order, but the flow of the screen reader cursor is not directly influenced by tabbability. 

Unlike the tabbing cursor, the existence, position and state of a screen reader cursor is not represented in the browser in any way. Although the screen reader cursor does move with the standard browser tab cursor, it can also be directed independently of it. When the tab cursor is moved, the screen reader cursor follows. But when the screen reader cursor moves, the tab cursor will not follow.

The screen reader cursor will read all readable text blocks and any additional information supplied to the cursor about the ownership, form, intent and behaviour of the readable element.

It is possible to declare elements and their descendants inaccessible to the screen reader. By setting an `[aria-hidden="true"]` attribute value on an element, the parent and its entire descendant tree becomes inaccessible. Elements which are `{ visibility: hidden; }` or `{ display: none; }` will also go unrepresented by a screen reader. Off screen, transparent or tiny elements remain readable and can be read (with variation) by different screen readers.

By default, a screen reader changes the behaviour of the keyboard in such a way that it becomes the primary method through which the user interacts with the computer. There are distinct and sometimes automatic [modes](https://www.accessibility-developer-guide.com/knowledge/screen-readers/desktop/browse-focus-modes/) assigned to key presses which allow for various tasks, such as navigation, text input and item selection. Keyboard shortcuts are an essential navigational tool for users who need to build a picture of graphically orientated content as a supplement to or in lieu of direct sight perception.

**Reference:** [Accessibility Developer Guide - Screen readers' browse and focus modes](https://www.accessibility-developer-guide.com/knowledge/screen-readers/desktop/browse-focus-modes/)

## New and built-in behaviours
### Focus control
#### Readability, focus and seeking forward
It is sometimes necessary to move browser tab focus (and hence the screen reader cursor), either to return the user to a previous location or to assist in the navigation of more complicated content presentations, such as accessing the non-active items in a narrative component.

The Adapt Framework can be reasonably modified and contains some complicated or changing user interface sequences. Programmatically assigning focus to an element that may become disabled or removed (due to user interaction or developer modification) will cause the screen reader cursor to drop to the document body instead. When the focus and screen reader cursor drop to the document body unexpectedly, the user loses their place in the document. The submit and feedback buttons are good examples of an Adapt Framework user interface which expresses many behavioural variations.

The Adapt Framework has two functions to aid in the allocation of focus, both of which seek forward in the document and assess the readability of elements as they go.

[`$("selector").focusOrNext();`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/libraries/jquery.a11y.js#L263-L278) Will try to focus on the selected element; on failing readability tests it will focus on the first readable child, or then the next readable element in the document.

[`$("selector").focusNext();`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/libraries/jquery.a11y.js#L249-L261) Will focus on the first readable child or the next readable element in the document.

These behaviours allow us to more loosely move the screen reader cursor and focus, relying on Adapt Framework to handle the correct allocation for us.

**Note:** Sometimes the next readable element cannot have focus assigned because it is not tabbable. If so, the Adapt Framework will temporarily add [`[tabindex=-1][data-ally-force-focus]`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/libraries/jquery.a11y.js#L228-L247) to the element, allowing it to receive focus as needed and then remove these attributes on blur.

#### Self-disabling buttons
The Adapt Framework occasionally makes use of functionality we call a 'self-disabling button'. The Submit button used in question components is a good example of this.

Disabled elements cannot receive the screen reader cursor or browser focus. When elements transition from having the focus of both the screen reader cursor and the browser to a disabled state, the screen reader cursor is moved by the screen reader to the document body. As described in the previous section, this isn't something you want to happen to a screen reader user.

Adapt Framework prevents the screen reader cursor from returning to the document body for self-disabling elements as it listens to blur events from elements with a `[disabled]` attribute and [moves the cursor on to the next readable element in the document](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/libraries/jquery.a11y.js#L513-L530). This retains the forward momentum of the content whilst allowing for self-disabling buttons.

#### Clicking with the keyboard
When 'clicking' any element with the <kbd>space</kbd> or <kbd>enter</kbd> keys whilst the screen reader is running, the 'clicked' element will not receive focus but will fire a `click` event. Clickable elements often act as the point of return from popups or other activities, this lack of focus assignment on click can be somewhat problematic when we need to be aware of the last active element.

Adapt helps mitigate the lack of focus on screen reader keyboard 'clicks' by using a capture event handler to [force focus when tabbable elements are clicked](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/libraries/jquery.a11y.js#L488-L497). This behaviour allows [`document.activeElement`](https://developer.mozilla.org/en-US/docs/Web/API/DocumentOrShadowRoot/activeElement) to work as one would expect it to with a mouse.  
References: [javascript.info - Bubbling and capturing events](https://javascript.info/bubbling-and-capturing)

### Roles (Regions)
[Navigation](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/navigationView.js#L23), [menu](https://github.com/adaptlearning/adapt-contrib-boxmenu/blob/master/js/adapt-contrib-boxmenu.js#L14), [page](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/pageView.js#L12), [notify](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/notifyView.js#L14) and [drawer](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/drawerView.js#L11) content is now assigned an appropriate
aria-role. This affords screen reader users easily distinguishable areas of the Adapt Framework user interface. Screen reader users can now cycle through the regions, giving them a sense of the user interface and allowing them to locate content with greater ease.

**Note:** A [component can optionally have a region](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/componentView.js#L14) by setting [`"_isA11yRegionEnabled": true`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/models/adaptModel.js#L14) on its model. This attribute is not yet represented in the schemas for the Authoring Tool as it is currently difficult to quantify its usefulness.

### Headings
Menu, page, article, block and component headings are set up to provide a more useful navigation layer for screen reader users. Headings now provide an extension to the header text by including a representation of the model's completion attribute along with an appropriate heading level.

Any view which triggers a `menuView:render`, `pageView:render`, `articleView:render`, `blockView:render` or `componentView:render` event and which contains an element with the class `js-heading` will now have a new [`HeadingView`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/headingView.js) injected into it.

[`HeadingView`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/headingView.js) is a visually hidden aria label; its text is transparent, tiny and absolutely positioned so that it is only read by the screen reader. Any visual representation of the heading text should therefore be hidden from the screen reader with an `[aria-hidden="true"]` attribute. This is so that the heading text will not be read twice by the screen reader.  
See: [`component.hbs`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/templates/partials/component.hbs#L8-L13) as an example.  

#### Heading completion settings
* model: `_disableAccessibilityState: false` Will enable/disable the `HeadingView` render
* model: `_isA11yCompletionDescriptionEnabled: true` Will cause the `HeadingView` to render the completion description
* course.json: `_globals._accessibility._ariaLabels.complete: "Completed"`
* course.json: `_globals._accessibility._ariaLabels.incomplete: "Incomplete"`

#### Heading attribute helper

Additional to and utilised by the HeadingView is the heading attribute helper `{{a11y_attrs_heading 'componentItem'}}`. This helper will produce the role and default heading level attribute for an element. The default heading level is taken from the map in `config.json: _accessibility._ariaLevels`. If the appropriate `_ariaLevel` value is found in the current context, it overwrites the default. This behaviour allows menu, page, article, block and component default heading levels to be controlled from `config.json` and also to be overridden on each model.

**Note:** ~~`_ariaLevel` is not yet defined in the Authoring Tool schemas.~~ Fixed in [AAT v0.6.3](https://github.com/adaptlearning/adapt_authoring/tree/v0.6.3)

#### Level settings
* config.json: `_accessibility._ariaLevels: { componentItem: 5, ... }`
* model: `_ariaLevel: 0`

**Note:** ~~Notify will always have heading level 1 since it is the only content represented on screen when active.~~ As of [v4.3.0](https://github.com/adaptlearning/adapt_framework/releases/tag/v4.3.0) the Notify heading level can now be set via `config.json`

### Invisible labels
The Adapt Framework has a couple of template helpers functions which allow a developer to provide additional screen reader-only text labels for the user. These labels are visually hidden; their text is transparent, tiny and absolutely positioned so as not to influence the document flow.

`{{a11y_aria_label 'text'}}` Will create a hidden text label.

`{{a11y_aria_image 'alt text'}}` Will create a fake image label, so that a background image or content image label need to be represented out of place.

References: [W3C - Invisible labels](https://www.w3.org/WAI/GL/wiki/Using_aria-label_to_provide_an_invisible_label)

### Component descriptions
Generic invisible label descriptions are defined by and enabled on each component. They appear under the component heading and are designed to help users understand how to interact with the user interface by providing a simple name and description of its behaviour. 

Component descriptions can be disabled by setting [`"_isA11yComponentDescriptionEnabled": false`](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/models/componentModel.js#L10) on the component models.

**Note:** `_isA11yComponentDescriptionEnabled` is not yet defined in the Authoring Tool schemas.  
See: [`narrative\properties.schema`](https://github.com/adaptlearning/adapt-contrib-narrative/blob/master/properties.schema#L10) as an example  

### Popups
When a modal popup, such as Notify or Drawer, is displayed, the user's actions should be restricted to just the popup content. With browsers and screen readers there are two ways of navigating to content under a modal popup: via tabbing and via the screen reader cursor.

#### Content restrictions
To prevent users from accessing content outside of the modal popups, Adapt Framework can restrict both the tabbing and screen reader cursor, isolating the user to just the popup content.

`Adapt.trigger("popup:opened", $popupElement);` will restrict the tabbing and screen reader access to just the element provided.

`Adapt.trigger("popup:closed", $focusTarget);` will revert the tabbing and screen reader access and move the focus to the element provided.

**Note:** Notify and drawer both use this soft API to control content access and require no additional configuration. This API will be turned into a hard API at some point in the near future.

#### Tab wrapping
To enable 'tab wrapping' - where tabbing beyond the popup will return the user to the first tabbable element in the popup - add `{{{a11y_wrap_focus}}` to the end of your popup template.

**Note:** Notify and Drawer both already implement this API and so require no additional modifications. Making use of these is therefore highly recommended.

### Navigation
#### Links vs buttons
Buttons and links which change the browser URL and/or load new content (that isn't a modal popup) should have an implied or declared [`[role="link"]`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_link_role) attribute.

Adapt Framework v4 applies this principle throughout by having [`[role="link"]`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_link_role) on all navigation buttons.

**Reference:** [Mozilla - MDN - Using the link role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_link_role)

### Scrolling
As focus moves through the document and on to elements which overflow the viewport, the browser will tend to scroll the subject elements into the viewport.

Adapt Framework v3 has a top navigation bar which overhangs the scrollable area of the viewport, obscuring any content beneath it. As the browser is both unaware of the navigation bar's obscuring of content and of the location of the screen reader cursor, the browser tends to scroll overflowing content underneath the navigation bar when bringing it into the viewport.

Adapt Framework v4 therefore introduces an additional configuration option which introduces a scrollable area _beneath_ the navigation bar. Enabling this allows the browser to scroll Adapt content in a way which does not allow any content to be obscured by the navigation bar, which is preferable for screen reader access.

* `config.json: _scrollingContainer._isEnabled = true` Enable the scrolling container
* `config.json: _scrollingContainer._limitToSelector = ""` Selectively apply the scrolling container according to this html tag selector. Useful for device targeting: `".os-windows.chrome, .os-windows.ie.version-11-0"`

**Note:** the downside of enabling `_scrollingContainer` is that it will disable some functionality of mobile browsers. For example, on Safari for iOS, the address bar will not shrink in size when you scroll down the page, nor will the 'double-tap the top of the screen to scroll to top' functionality work.

Table showing the use cases for alternative scrolling:
<table>
<tr>
<th></th><th>Screen reader</th><th>iOS iframe</th><th>Browser gestures</th>
</tr>
<tr>
<td>
<pre>"_scrollingContainer": {
    "_isEnabled": false,
    "_limitToSelector": ""
}</pre></td>
<td>❎</td>
<td>❎</td>
<td>✅</td>
</tr>
<tr>
<td><pre>"_scrollingContainer": {
    "_isEnabled": true,
    "_limitToSelector": ""
}</pre></td>
<td>✅</td>
<td>✅</td>
<td>❎</td>
</tr>
<tr>
<td><pre>"_scrollingContainer": {
    "_isEnabled": true,
    "_limitToSelector": ".os-ios"
}</pre></td>
<td>❎</td>
<td>✅</td>
<td>✅ (Not on iOS)</td>
</tr>
<tr>
<td><pre>"_scrollingContainer": {
    "_isEnabled": true,
    "_limitToSelector": 
     ":not(.os-android)"
}</pre></td>
<td>✅</td>
<td>✅</td>
<td>✅ (Android only)</td>
</tr>
</table>

### Screen-reader-specific text
Occasionally, screen readers like Jaws do not read out the on-screen text correctly - and changing it to suit Jaws may not always be an option. The classic example is Jaws reading 'IT' as 'it' rather than 'eye tea'. As a workaround, Adapt v4.4.0 introduced the `ally_text` handlebars helper which can be used to give screen readers a different version of the text to read out, for example: `{{a11y_alt_text 'IT' 'I T'}}` or `{{a11y_alt_text '$5bn' 'five billion dollars'}}`

### Browser and screen reader compatibility
Accessibility in Adapt Framework v4 has been built with the following screen readers, browsers and operating systems in mind:

* JAWS 18+ and IE11 on Windows (primary testing target)
* JAWS 18+ and Chrome on Windows (used in development process)
* Voiceover and Chrome on OSX (used in development process)
* NVDA and Firefox ESR on Windows (untested at present)

**Note:** 'Evergreen' Firefox is currently having accessibility issues despite being one of the most requested browsers for corporate e-learning accessibility.

### Exceptions to the WCAG implementation examples
#### Headings
In lieu of semantic `h` tags (`<h1>`, `<h2>` etc.) Adapt uses `role="heading"` and `aria-level="1"` attributes. This is because we use classes to style heading texts and templates+JSON to define the heading level throughout the framework, which makes using semantic `h` tags unfeasible. The `role="heading"`, `aria-level="1"`attribute syntax is very well supported and an acceptable alternative for semantic `h` tags. However, it is a relatively new technique, and some older accessibility testing tools/documentation may incorrectly flag it as an issue.

**Reference:** [W3C - WCAG Technique - ARIA12](https://www.w3.org/TR/WCAG20-TECHS/ARIA12.html)

#### Alternative text
Instead of using `<img alt="text">` we use `<img aria-label="text">`. The `aria-label` attribute supersedes the `alt` attribute and is common to all elements in the DOM as well as being very well supported. The `alt` attribute is only available on the `<img>` tag and so should be thought of as a legacy attribute. 

As with the use of `role="heading"` attribute, some older accessibility testing tools/documentation may incorrectly flag the lack of `alt` attributes as an issue. No matter how commonplace is the message that 'images must have alt tags in order to be accessible,' it is no longer accurate. Likewise, confusion persists between the `alt` attribute and a visual “tooltip” that appears when hovering over an image.

**References:** [W3C - WCAG Technique - ARIA6](https://www.w3.org/TR/WCAG20-TECHS/ARIA6.html), [Mozilla - MDN - ARIA:img role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Role_Img), [W3C - WAI-ARIA 1.0 User Agent Implementation Guide](https://www.w3.org/TR/2014/REC-wai-aria-implementation-20140320/#mapping_additional_nd_name), [W3C - HTML Accessibilty API Mappings 1.0 - Draft](https://www.w3.org/TR/html-aam-1.0/#img-element)


### References
#### JAWS keyboard controls
* <kbd>&uarr;</kbd> = move backward
* <kbd>&darr;</kbd> = move forward
* <kbd>space</kbd> = make selection
* <kbd>space/return</kbd> = click
* <kbd>h</kbd> = cycle through headings
* <kbd>r</kbd> = cycle through regions
* <kbd>q</kbd> = go to main content
* <kbd>esc</kbd> = exit selection (forms mode) or dismiss notify


#### Sources
* [W3C - Web content accessibility guidlines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [W3C - How to meet WCAG 2 (Quick reference)](https://www.w3.org/WAI/WCAG21/quickref/)
* [tink.uk - Understanding screen reader interaction modes](https://tink.uk/understanding-screen-reader-interaction-modes/)
* [javascript.info - Bubbling and capturing events](https://javascript.info/bubbling-and-capturing)
* [Accessibility Developer Guide - Screen readers' browse and focus modes](https://www.accessibility-developer-guide.com/knowledge/desktop-screen-readers/browse-focus-modes/)
* [Freedom Scientific - JAWS 2019](https://www.freedomscientific.com/Downloads/JAWS/JAWSWhatsNew)
* [WebAIM - Keyboard shortcuts for JAWS](https://webaim.org/resources/shortcuts/jaws)
* [NV Access - About NVDA](https://www.nvaccess.org/about-nvda/)
* [Mozilla - Firefox ESR](https://www.mozilla.org/en-US/firefox/organizations/)
* [W3C - WCAG Technique - ARIA6](https://www.w3.org/TR/WCAG20-TECHS/ARIA6.html)
* [W3C - WCAG Technique - ARIA12](https://www.w3.org/TR/WCAG20-TECHS/ARIA12.html)
* [Mozilla - MDN - ARIA:img role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Role_Img)
* [Mozilla - MDN - Using the link role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_link_role)
* [W3C - WAI-ARIA 1.0 User Agent Implementation Guide](https://www.w3.org/TR/2014/REC-wai-aria-implementation-20140320/#mapping_additional_nd_name)
* [W3C - Accessibilty API Mappings 1.0 - IMG Element - Draft](https://www.w3.org/TR/html-aam-1.0/#img-element)
* [W3C - Invisible labels](https://www.w3.org/WAI/GL/wiki/Using_aria-label_to_provide_an_invisible_label)



