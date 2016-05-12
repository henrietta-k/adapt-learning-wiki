# Accessibility
- [What is meant by accessibility?](#what-is-meant-by-accessibility) 
- [For the learner: How does the accessibility feature function in Adapt?](#how-does-the-accessibility-feature-function-in-adapt)
- [For the course author: Make your course accessible.](#make-your-course-accessible)  
- [For the plug-in developer: Make your plug-in accessible.](#make-your-plug-in-accessible)  
- [Resources](#resources)

## What is meant by accessibility? 

Accessibility is a short way of referring to:   
- the features in Adapt that make content usable to persons with low- or no-vision and to those who do not use a mouse;
- industry standards such as the W3C's [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/intro/wcag)
- [government regulations](http://www.powermapper.com/blog/government-accessibility-standards/) such as the Equality Act in Europe, BS 8878:2010 in the UK, and section 508 in the US.  

The goal of Adapt's accessibility feature is to aid users and screen readers by making every piece of content keyboard-accessible and readable. The rationale behind it is to ensure the Adapt framework adheres to the W3C2 AA standards
where possible.  

## How does the feature function in Adapt?  

All Adapt courses have the accessibility feature built-in. However, it must be enabled during development by the course author before the course is published. Once the course is published, the feature remains hidden until it is activated by the learner.

To activate the accessibility feature while viewing a course, press the Tab key. A button is displayed: "Turn accessibility on?". Press the Enter/Return key. (If the Enter/Return key is not pressed, the button will continue to display until tabbing encounters the first element in the page that is natively keyboard accessible.)

Once the feature is activated, pressing the Tab key navigates the learner through content. Focused content regions are highlighted with an outline. And ARIA labels are enabled for assistive technology such as screen readers.  
<div float align=right><a href="#top">Back to Top</a></div>  
-----
## Make your course accessible.  

The course author can ensure a course is accessible by taking several steps:  
- [Enable accessibility](#enable-accessibility)
- [Use plug-ins that support accessibility](#use-plug-ins-that-support-accessibility)  
- [Add *_global* ARIA labels for non-core plug-ins](#add-_global-aria-labels-for-non-core-plug-ins)  
- [Attend to images: alt text](#alt-attribute)
- [Attend to images: `no-state`](#no-state-class)
- [Attend to inaccessible components: `not-accessible`](#not-accessible-class)

### Enable accessibility

- To enable accessibility in a course while working in the Adapt authoring tool, set accessibility to true in the Project Settings.  
- To enable accessibility while working in the Adapt framework, set `"_isEnabled"` to true within the `"_accessibility"` section of *config.json*. If accessibility is not enabled, the learner cannot activate the feature.

### Use plug-ins that support accessibility  

All plug-ins (components, extensions, menus, and themes) bundled with the Adapt framework and authoring tool support accessibility. This means their code includes [ARIA roles, regions, and labels](https://www.w3.org/WAI/intro/aria) and supplements tab indexes where necessary. 

You cannot assume that a third-party plug-in adequately supports accessibility. Look for evidence in the following.
- **_README.md_**. Chances are you located the plug-in either through the Adapt community [Plug-in Browser](https://www.adaptlearning.org/index.php/plugin-browser/) or by [searching GitHub](https://github.com/search?l=JavaScript&q=adapt-&type=Repositories&utf8=%E2%9C%93) repositories. Either way makes it easy for you find and review the repository's README. Look for notice of accessibility support or mention of WAI AA or WCAG.  
- **Code**. Look in the plug-in's template for ARIA. You don't need to know JavaScript. Here's what you do:  
    1. In the plug-in's GitHub repository, open the folder named *templates*. There you will find one or more files whose name ends with the *.hbs* extension. Open each file in GitHub and examine its content (no need to download it).
    2. Look for phrases that begin with `aria-`, such as `aria-region`, `aria-role`, and `aria-label`. Also look for the presence of `a11y_text`. This is evidence that the developer has made an effort to support Adapt accessibility features. It is no guarantee that the effort was successful, but the plug-in meets the basic requirement for testing.   

### Add *_global* ARIA labels for non-core plug-ins  

The bulk of Adapt course content is found in presentation components and question components. The sighted learner has the ability to scan the page to determine what next step she'll take to access the content. Because low-vision can impede this ability, each component presents an `aria-label` that describes how it functions. ARIA labels are not visible; they are announced by screen readers. Regardless of how many times a particular component is used within a course, the same description of it is announced to the learner.    

The Adapt framework gathers these descriptions in the *course.json* file in a section called [`"_globals"`](Globals-and-ARIA-Labels). You'll find the same descriptions in the Adapt authoring tool in the Accessibility section of the Project configuration menu. Adapt provides descriptions for the core plug-ins. It cannot provide descriptions for plug-ins it does not about. If you use a third-party plug-in AND if the accessibility feature is important to your learners, ensure your plug-in has an entry in `"_globals"`.  
<div float align=right><a href="#top">Back to Top</a></div>


### Attend to images  

#### alt attribute  

All images should have an alt attribute. The value assigned to this attribute is often called "alt text". Whether or not the alt attribute is assigned alt text depends on the purpose of the image. Nonetheless, the alt attribute should be present in all cases, even if it is not assigned a value, e.g., `alt=""`.

Graphics in courses fall into two broad categories: images that convey course content and those that don't. Focus on those that do. Decide which images represent information significant to the content. Assign alt text to these images. Balance your decisions with a recognition of the additional time it will take your visually impaired learner to scan through the page. For example, alt text that describes the physical characteristics of your course avatar may have significance for some topics but not for others.

Give care to charts and diagrams. If an adequate description and interpretation is provided in the text, it is possible that no alt text is needed. 

>Note: Often confused with the alt attribute, the [title](http://www.w3schools.com/tags/att_global_title.asp) attribute plays a minor role in accessibility. It can hinder efforts to be accessible if employed improperly. 

#### `no-state` class  

All components that conform to Adapt standards by extending the [*componentView.js*](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/componentView.js) report their state&mdash;complete or incomplete&mdash;in ARIA labels. This is achieved through [*state.hbs*](https://github.com/adaptlearning/adapt-contrib-vanilla/blob/master/templates/partials/state.hbs) which *componentView.js* automatically appends to the component. 

Reporting state is necessary for components that are interactive. But reporting state for those that are not, such as [adapt-contrib-blank](https://github.com/adaptlearning/adapt-contrib-blank/blob/master/js/adapt-contrib-blank.js) and [adapt-contrib-graphic](https://github.com/adaptlearning/adapt-contrib-graphic), is unnecessary and may even distract the learner.

To override this default behaviour, add the class `no-state` to the non-interactive component. This class has no inherent impact on CSS styles. Instead, its presence prevents [*state.hbs*](https://github.com/adaptlearning/adapt-contrib-vanilla/blob/master/templates/partials/state.hbs) from being added to the component. [adapt-contrib-blank](https://github.com/adaptlearning/adapt-contrib-blank/blob/master/js/adapt-contrib-blank.js) automatically adds the class to itself. [adapt-contrib-graphic](https://github.com/adaptlearning/adapt-contrib-graphic/blob/master/js/adapt-contrib-graphic.js) *does not*. Although rare, there may be scenarios in which it is important to track whether an image and/or its alt text have been presented to a learner. A clue may be whether you are tracking the image with [adapt-contrib-pageLevelProgress](https://github.com/adaptlearning/adapt-contrib-pageLevelProgress) for sighted learners. For this reason, `no-state` is **_not_** automatically added to **Graphic**. If **Graphic** and its alt text do not contribute significant content to the course, it is recommended to assign it the class `no-state`.

#### `not-accessible` class

Some components can never be accessible. Components which rely on making sighted judgments or which require a level of visual special awareness can be skipped over when the course has accessibility enabled. To achieve this, assign the component the class `not-accessible`. Doing that will remove the component from the tabbing order. Be sure to configure these components as [optional](https://github.com/adaptlearning/adapt_framework/wiki/Core-model-attributes), since they will never be completed by the learner who relies on tabbing.  
<div float align=right><a href="#top">Back to Top</a></div>
-----
## Make your plug-in accessible.  

The plug-in developer can ensure a component is accessible by taking several steps: 
- [Extend *componentView.js*](#extend-componentviewjs)
- [Add ARIA roles and labels](#add-aria-roles-and-labels)
- [Process text with `a11y_text`](#process-text-with-a11y_text)
- [Provide sample text for `_globals`](#provide-sample-text-for-_globals)

### Extend *componentView.js*  

Extending [componentView.js](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/views/componentView.js) is the first step in ensuring your component integrates Adapt's accessibility feature.  
``` javascript  
//Code snippet of extending componentView: 
define(function(require) {
    var ComponentView = require('coreViews/componentView');
    var Adapt = require('coreJS/adapt');
    var HotGraphic = ComponentView.extend({
```
<div float align=right><a href="#top">Back to Top</a></div>  

### Add ARIA roles and labels to your template  
Your plug-in's HTML will be read by assistive technology such as screen readers. Most widgets require additional attributes to facilitate this. Add them to your plug-in's Handlebars (.hbs) template. [ARIA roles and labels](https://github.com/adaptlearning/adapt_framework/wiki/ARIA-Roles-and-Labels) provides a useful summary.   
``` javascript  
//Example of ARIA role and aria-label: 
<div class="mynewcomp-inner component-inner" role="region" aria-label="{{_globals._components._mynewcomp.ariaRegion}}">
```  
>**Essential technical guidance** can be found in three documents:  
    - [*The Adapt Accessibility Standards and Guidelines*](https://github.com/adaptlearning/documentation/blob/master/04_wiki_assets/adapt_framework/Adapt-Accessibility-OS-Doc.pdf) provides instruction and examples useful for implementing ARIA in templates.   
    - [jquery.a11y README](https://github.com/adaptlearning/jquery.a11y) provides usage examples, functions references, and style descriptions.   
    - [*Accessibility in Adapt: A Technical Perspective*](https://github.com/adaptlearning/documentation/blob/master/04_wiki_assets/adapt_framework/accessibility-notes.pdf) provides information about the properties, methods, and events found in [accessibility.js](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/js/accessibility.js) and [jquery.a11y.js](https://github.com/adaptlearning/jquery.a11y).  

### Process text with `a11y_text` 
Course authors may include HTML tags in their text content. Sometimes it is welcomed and extends the plug-in's usefulness. Sometimes it undermines accessibility. Some HTML elements, such as `<div>` and `<span>`, do not have a natural ability to receive focus. This removes them from the tabbing order and makes their content unreachable by screen readers. You can make such content keyboard-accessible and accessible by processing it with `a11y_text`.  `a11y_text` is a function found within Adapt's *jquery.a11y.js*. Implement it in your template as in the model below:  
``` javascript  
//Example of processing body text with a11y_text:  
<div class="mynewcomp-content-body-inner">{{{a11y_text body}}}</div>
```  
  
<div float align=right><a href="#top">Back to Top</a></div>

### Provide sample text for `_globals`
The sighted learner can scan a plug-in to determine how to interact with it. The learner who relies on a screen reader requires a description of the component or an instruction to know how to interact with it. Your plug-in should provide this description in an aria-label that is associated with `role="region"` and that is located in your component's root div. Reference the template of any of Adapt's [core components](https://github.com/adaptlearning/adapt_framework/wiki/Core-Plug-ins-in-the-Adapt-Learning-Framework#components) for a model. 

You could hard-code the description and instruction into the aria-label, but it is not recommended. Adapt encourages exposing the text to editing by the course author in case customisation is desirable. To expose it to editing in the Adapt authoring tool, add a `"globals"` section to your [*properties.schema*](https://github.com/adaptlearning/adapt_authoring/wiki/Properties-Schema#globals). To expose it in Adapt's framework, the [course author will need to enter it](#add-_global-aria-labels-for-non-core-plug-ins) into the `"_globals" section of *course.json*. You can make it easy, since you know your plug-in so well, by supplying suggested text in your *example.json*. The value for `"ariaRegion"` should include a succinct description and how to interact with it:  
``` javascript  
//Add the _mynewcomp section to the _globals in your course.json:  
"_globals": {
        "_components": {
            "_mynewcomp": {
                "ariaRegion": "This component is made up of things that do this and that. Select the thingamajig to access the content.",
                "instruction": ""
            },  
```

### Inaccessible plug-ins

Some components can never be accessible. Those which rely on making sighted judgments or those
components which require a level of visual special awareness should be specifically labeled as
inaccessible. To mark a plug-in as inaccessible, add the following line of code to the plug-in's `preRender` function:  
``` javascript  
preRender: function() {
    this.$el.addClass("not-accessible");
    // other code
},
```
-----
## Resources
 
- [WAI-ARIA Overview (W3C)](https://www.w3.org/WAI/intro/aria)
- [HTML5 Accessibility Chops: hidden and aria-hidden (The Paciello Group)](https://www.paciellogroup.com/blog/2012/05/html5-accessibility-chops-hidden-and-aria-hidden/)  
- [Name, State, Role, and Value: What’s it all about? (Karl Groves)](http://www.karlgroves.com/2013/03/02/name-state-role-and-value-whats-it-all-about/)
- [Accessibility: worked example](https://github.com/adaptlearning/adapt_framework/wiki/Accessibility:-worked-example)