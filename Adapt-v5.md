## Overview
Adapt v5 aims to make it easier to read and write the Adapt framework and plugins by introducing **BEM**, a new naming convention, and **SMACSS**, a modular approach to front-end code.

## What has changed

### CSS naming and architecture 

V5 has moved toward a CSS naming convention and structure based on BEM and SMACCS principles to ensure the code is uniform, modular and reusable. Component classes now follow a BEM-inspired convention of .block__modifier, reducing nesting and clearly defining their relationship to the component and its structure. Modifiers are separated from these component classes and take the form of 'action' identifiers, such as 'is-visited', to clarify their purpose. 

Examples: 

.article__header

.article__header-inner

is-visited

LESS usage: 

.article {

  &__header.is-visited {}

  &__header-inner {}

}

Core framework CSS now includes files for utility, layout and base classes following SMACSS recommendations for class categorisation. Layout classes are prefixed with .l- (e.g., .l-container-responsive) and utility classes begin with .u- (e.g., .u-display-none). Utility classes are those that serve a single purpose and are named as such for easy reuse. 

.u-display-none {

  display: none;

{

Core variable declarations have been reduced so as not to require heavy overriding in theme, and reset.less has been switched to normalize.less for increased cross-compatibility. 

### CSS approach 

CSS in both core and plugins has been modernised and stripped back to serve only structure and functionality, leaving styling to the theme, which will remove redundancy and prevent conflict and the need for multiple overrides. Adapt now uses rem rather than pixels as the base measurement, which increases support for cross-browser zoom and font size settings and improves accessibility. 

Whereas previously the JavaScript made use of existing styling classes, these have now been decoupled into, where possible, JavaScript hooks and separate classes for styling alone.  

.nav__back-btn.js-nav-back-btn

### Spacing and indentation 

Spacing and indentation has been made consistent throughout Adapt files using two spaces for indentation rather than tabs. The exception to this is that json files have retained four-space indentation. 