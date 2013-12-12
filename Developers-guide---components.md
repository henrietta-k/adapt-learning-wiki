#### What is a component

In Adapt we have a concept of components. These components are the main interactive elements found on a page. (Multiple Choice Question, Media, Text and Narrative are all types of components). These components can be split into two categories.

#### Presentational components

A presentational component should be used to display content with little interactivity. A few components that full under this category are: Graphic, Media, Hot Graphic and Narrative. Each presentational component should set the following on it's model:

- ``_isComplete`` (boolean) - Should be set on the model when the user completes the question and used all the avilable attempts.
- ``_isReady`` (boolean) - Should be set on the model when the component is fully loaded. If this the component has imagery please see the adapt-contrib-narrative component for an exmaple of imageReady.

#### Question components

A question component should be used to test a user or ask a question. Each question component should set the following on it's model:

- ``_isPassed`` (boolean) - Should be set on the model when the user gets this question correct.
- ``_isComplete`` (boolean) - Should be set on the model when the user completes the question and used all the avilable attempts.
- ``_isReady`` (boolean) - Should be set on the model when the component is fully loaded. If this the component has imagery please see the adapt-contrib-narrative component for an exmaple of imageReady.
- ``_weight`` (boolean) - Each question component should have a weight. This is either taken from the global ``_weight`` attribute or from the components individual ``_weight`` attribute.

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

Classes should be descriptive and prefixed with the components name. All Less styling should be laid out in the following format, where an initial nested class is used to hold everything to do with the component. The only styling outside of this should be the ``.no-touch`` class (used for adding hovers on elements for devices that are not touch).

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

##### Assets

All assets for a component should be prefixed with the component name:

``media-flashPlayer.swf``

##### JSON

###### schema.json

This file is needed for the component to work with the editor. It describes what fields are needed to edit the component.

###### example.json

Each component should come with an example.json which contains an example of the data structure needed for this component to work. This enables developers to copy this over without the need for an editor.

#### Preset methods

Each component has the following preset methods:

- ``setReadyStatus`` - Sets the component to ready.
- ``setCompletionStatus`` - Sets the component to complete.
- ``init`` - Should be used to setup anything before render.
- ``postRender`` - Should be used to setup anything after render.
- ``events`` - Should be used to attach events on the component.


##### Question components