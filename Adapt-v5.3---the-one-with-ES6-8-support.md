### What has changed?
For a long time Adapt Framework ECMAScript support has been limited by our minimum supported browser, most recently IE11,  however it is now possible to use [ES6](https://exploringjs.com/es6/), [ES7 and ES8](https://exploringjs.com/es2016-es2017/) in large parts of Adapt Framework whilst retaining IE11 support. 

#### How?
We still use [requirejs](https://requirejs.org/) to [bundle](https://www.freecodecamp.org/news/javascript-modules-part-2-module-bundling-5020383cf306/) our modules but rather than using [UglifyJS](https://github.com/mishoo/UglifyJS) for minification, which supports up to ES5, we now use [Babel](https://babeljs.io/) for minification and for transpilation and we transpile from ES6-8 to IE11 supported ES5.

#### Why stop at ES8?
[Babel](https://babeljs.io/) supports ECMAScript beyond ES8 but our module bundler [requirejs](https://requirejs.org/) uses [esprima](https://github.com/jquery/esprima/blob/master/README.md) to parse ECMAScript and esprima only supports up to ES8. Introducing ES6-8 using this pathway should allow scope for parallel works to continue rather than converting the Adapt Framework and its build system in one go. We can now move towards replacing our build system in future versions whilst providing space for the community to modernise and refactor the Adapt Framework using much newer ECMAScript standards.

#### Limitations
* You can **only** use ES6-8 in the `/js/` folder of the core and plugins.
* The `/required/` folder, the `/libraries/` folder and externally required modules **do not** support ES6-8 as these are not transpiled by our build process and will not work in IE11.
* You **should not** use the [`import` and `export` statements](https://exploringjs.com/es6/ch_modules.html) as we are still using [requirejs](https://requirejs.org/) as our module bundler.


### ES6 classes and Backbone
There are a few major concepts worth understanding before using [ES6 Classes](https://exploringjs.com/es6/ch_classes.html) and [Backbone](https://backbonejs.org/) together. Backbone is an ES5 library for providing an easy Class abstraction and a few base classes from which to extend and make new, easy to read behaviours. ES6 Classes are the standardised ECMAScript native Class abstraction. Both Backbone and ES6 Classes seek to provide Class abstractions in similar but subtly different ways.

#### ECMAScript Class origins
A Class in ECMAScript is simply a function called using the `new` keyword. This function is called the `constructor` function and is executed as usual using the `()` notation. When we call a function using the `new` keyword, an new object instance is created and passed into the function as its `this` keyword. We call this process instantiation - creating a new instance of the Class.
```js
var Class = function() { // constructor function
  this; // is a new instance of the class
};
var instance = new Class(); // instantiation
````
The new keyword allows us to specify a set of behaviours on the Class which each new object instance will inherit. These behaviours don't live on the instance directly but are instead inherited from the parent Class.
```js
var Class = function Constructor(text) {
  this.savedText = text;
  this.log(text);
};
Class.prototype.log = function(text) { console.log(text); };

var instance = new Class('test1');
instance.log('test2');

var instance2 = new Class('test3');
instance2.log('test4');
```
If you execute and inspect the above code in a debugger, you will see that `savedText` lives directly on the new instance, whereas `log` is inherited via the `__proto__` property. 

#### Inheritance chains
It is possible to create many layers of inheritance such that one class is able to inherit behaviour from another and all behaviour from all classes in the chain of inheritance will be expressed on the instance.
```js
var Class = function ConstructorA() {};
Class.prototype.log = function(text) { console.log(text); };

var Class2 = function ConstructorB() {};
Class2.prototype = Object.create(Class.prototype); // extend/inherit from the Class prototype
Class2.prototype.log2 = function(text) { console.log(`${text}2`); };

var instance = new Class2();
instance.log('test1');
instance.log2('test');
```

In the above example we can see that the instance inherits `log` from its grandparent and `log2` from is parent. It should be apparent by this point that the syntax is rather messy and unnecessarily complex.

##### So far....
We have the constructor function, the `new` keyword, the `this` keyword, the constructor's `prototype` object, the instance and the instance's prototype inheritance chain.

##### Pretty Classes
Backbone and ES6 classes are identical in the above regards but both provide a much nicer syntax for achieving the same ends.

Backbone:
```js
var Class = Backbone.Model.extend({ // returns a constructor function
  // defines the constructor.prototype object
  log: function(text) { console.log(text); }
});

var Class2 = Class.extend({
  log2: function(text) { console.log(`${text}2`); }
});

var instance = new Class2();
instance.log('test1');
instance.log2('test');
```
ES6:
```js
class Class {  // returns a constructor function
  // defines the constructor.prototype object
  log(text) { console.log(text); }
}

class Class2 extends Class {
  log2(text) { console.log(`${text}2`); }
}

var instance = new Class2();
instance.log('test1');
instance.log2('test');
```

#### Class static properties
Aside from being able to define constructor prototype behaviour for each instance, it is possible to assign properties directly to the Class, these are called static properties. Class static properties are often helpful for defining behaviour which belongs to a Class abstraction but which is not specific to an instance of the Class.
```js
var Class = function Constructor() {
  Class.recordInstances(); // record that a new instance was made
};

Class.instances = 0;
Class.recordInstance = function() {
  this.instances++;
};
```
Contrast [String.fromCharCode()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode) with [String.prototype.charCodeAt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt).

Natively Backbone and ES6 differ in the way they treat Class static properties. Backbone will copy the parent class static property values and assign them to the child class at the same property name, whereas ES6 will inherit parent class static properties on the child class.

In Adapt Framework we have a [polyfill](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/libraries/backbone.es6.js) that corrects the Backbone's static property behaviour and brings it inline with ES6 inheritance, such that parent class static properties are now inherited by the child class in Adapt Framework.

Backbone:
```js
var Class = new Backbone.Model.extend({
  // defines the constructor.prototype object
  log: function() {}
}, {
  // defines class static properties
  recordInstance() {}
});
```
ES6:
```js
class Class {
  // defines the constructor.prototype object
  log() {}
  // defines class static properties
  static recordInstance () {}
}

#### Practical differences between ES6 and Backbone classes
With Backbone classes it is possible to assign any value or reference to the constructor prototype object, but it more complicated to add a property getter/setter.
```js
var Class = Backbone.Model.extend({
  a: null,
  b: 1,
  c: "string",
  d: function() {},
  e: {},
  f: []
});

// getter/setter definition
Object.defineProperty(Class.prototype.g, {
  get: function() {
    return this._g;
  },
  set: function(value) {
    this._g = value;
  }
});
```