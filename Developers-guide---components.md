#### What is a component

In Adapt we have a concept of components. These components are the main interactive elements found on a page. (Multiple Choice Question, Media, Text and Narrative are all types of components). These components can be split into two categories.

#### Presentational components

A presentational component should be used to display content with little interactivity. A few components that full under this category are: Graphic, Media, Hot Graphic and Narrative.

#### Question components

A question component should be used to test a user or ask a question. Each question component should set the following on it's model:

- ``_isPassed`` (boolean) - Should be set on the model when the user gets this question correct.
- ``_isComplete`` (boolean) - Should be set on the model when the user completes the question and used all the avilable attempts.
- ``_isReady`` (boolean) - Should be set on the model when the component is fully loaded. If this the component has imagery please see the adapt-contrib-narrative component for an exmaple of imageReady.
- ``_weight`` (boolean) - Each question component should have a weight. This is either taken from the global ``_weight`` attribute or from the components individual ``_weight`` attribute.

#### Structure of components

#### Getting started

#### Naming conventions

##### Javascript

##### Less

##### Assets

##### JSON

###### schema.json

###### example.json