#### What is a component?

In Adapt we have a concept of components. These components are the main interactive elements found on a page. (Multiple Choice Question, Media, Text and Narrative are all types of components). These components can be split into two categories.

#### Presentational components

A presentational component should be used to display content with little interactivity. A few components that full under this category are: Graphic, Media, Hot Graphic and Narrative. Each presentational component should call the following methods in the view:

- ``setCompletionStatus`` - Should be called when the user completes the component.
- ``setReadyStatus`` - Should be called when the component is fully loaded. If the component has images, please see the adapt-contrib-narrative component for an example of imageReady.

#### Question components

A question component should be used to test a user or ask a question. Question components have the same methods presentation components have so they should be using ``setCompletionStatus`` and ``setReadyStatus``. Question components have a few extra methods available:

- ``getOptionSpecificFeedback``

- ``setupQuestion`` - This is called from the preRender method and is used to setup any question settings before rendering. This method is intended to be overwritten if needed

- ``_setupDefaultSettings`` - This is called from the preRender method and is used to setup default settings on the question like button text and question weight. This method calls other methods like ``setupButtonSettings`` and ``setupWeightSettings`` This method should remain as is.

- ``setupButtonSettings`` - This is called from setupDefaultSettings and sets whether the button text should be taken from the global button settings or from the components settings

- ``setupWeightSettings``
- ``resetQuestion``
- ``showFeedback``
- ``showModelAnswer``
- ``showUserAnswer``
- ``onComplete``
- ``onQuestionCorrect``
- ``onQuestionIncorrect``
- ``onModelAnswerClicked``
- ``onResetClicked``
- ``onSubmitClicked``
- ``onUserAnswerClicked``
- ``showInstructionError``

Each question component should also set the following on its model:

- ``_isCorrect`` (boolean) - This should be set when the question has no more attempts and the user has finished interacting with the question.

#### Structure of components

All components should have the following files to work:

- Javascript file (.js)
- Handlebars file for templates (.hbs)
- Less file for styling (.less)

There are other files such as our testing suite, bower.json file and LICENSE files. Please view the adapt-component repository

#### Getting started

#### Naming conventions

##### Javascript



##### Less

All css classes use a dashed approach:

``.text-component``

Classes should be descriptive and prefixed with the component's name. All Less styling should be laid out in the following format, where an initial nested class is used to hold everything to do with the component. The only styling outside of this should be the ``.no-touch`` class (used for adding hovers on elements for devices that are not touch).

````
.accordion-component {

  .accordion-item {
      border: 1px solid #b9b9b9;
      margin-bottom: 2px;
  }

  .accordion-item-icon {
      position: absolute;
      top: 50%;
      margin-top: -12px;
      left: 10px;
  }

  .accordion-item .selected .arrow-r {
      position: absolute;
      top: 50%;
      margin-top: -12px;
      left: 10px;
  }

  .accordion-item-title {
      position:relative;
      display:block;
      background-color:#fff;
      text-decoration: none;

      &.visited {
        background-color:#919191;
      }

      &.selected {
        background-color:#b9b9b9;
      }
  }

  .accordion-item-title-inner {
      padding:14px 14px 14px 42px;
      color:#454545;
  }

  .accordion-item-body {
      display:none;
      border-top: 1px solid #b9b9b9;
  }

  .accordion-item-body-inner {
      padding:14px;
  }

}

.no-touch {
  .accordion-component {
    .accordion-item-title {
      &:hover {
        background-color:#ccc;
        color:#fff;
      }
      &.visited:hover {
        background-color:#919191;
      }
    }
  }
}
````
###### Theme inheritence

All components should inherit from the theme. The following Less variables are available:

- ``@primary-color``
- ``@secondary-color``
- ``@tertiary-color``
- ``@foreground-color``
- ``@background-color``
- ``@inverted-foreground-color``
- ``@inverted-background-color``
- ``@transparency``
- ``@button-color``
- ``@button-hover-color``
- ``@button-disabled-color``
- ``@button-text-color``
- ``@button-text-hover-color``
- ``@button-text-disabled-color``
- ``@component-title-padding``
- ``@component-body-padding``
- ``@component-item-padding``
- ``@validation-error-text-color``
- ``@validation-error-icon-color``
- ``@validation-error-border-color``

##### Templates

##### Assets

All assets for a component should be prefixed with the component name:

``media-flashPlayer.swf``

##### JSON

###### properties.schema

This file is needed for the component to interface with the authoring tool. It describes the properties that need to be configured. The authoring tool uses this data to construct an interface to gather input from the course developer.

###### example.json

Each component should come with an example.json which contains an example of the data structure needed for this component to work. This enables developers to copy this over without the need for an editor.

#### Preset methods

Each component has the following preset methods:

- ``setReadyStatus`` - Sets the component to ready.
- ``setCompletionStatus`` - Sets the component to complete.
- ``preRender`` - Should be used to setup anything before render.
- ``postRender`` - Should be used to setup anything after render.
- ``events`` - Should be used to attach events on the component.

##### Question components