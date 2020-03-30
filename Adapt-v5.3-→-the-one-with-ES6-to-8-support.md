### What has changed?
For a long time Adapt Framework ECMAScript support has been limited by our minimum supported browser, most recently IE11,  however it is now possible to use [ES6](https://exploringjs.com/es6/), [ES7 and ES8](https://exploringjs.com/es2016-es2017/) in large parts of Adapt Framework whilst retaining IE11 support. 

#### How?
We still use [requirejs](https://requirejs.org/) to [bundle](https://www.freecodecamp.org/news/javascript-modules-part-2-module-bundling-5020383cf306/) our modules but rather than using [UglifyJS](https://github.com/mishoo/UglifyJS) for minification, which supports up to ES5, we now use [Babel](https://babeljs.io/) for minification and for transpilation and we transpile from ES6-8 to IE11 supported ES5.

#### Why stop at ES8?
[Babel](https://babeljs.io/) supports ECMAScript beyond ES8 but our module bundler [requirejs](https://requirejs.org/) uses [esprima](https://github.com/jquery/esprima/blob/master/README.md) to parse ECMAScript and esprima only supports up to ES8. Introducing ES6-8 using this pathway should allow scope for parallel works to continue rather than converting the Adapt Framework and its build system in one go. We can now move towards replacing our build system in future versions whilst providing space for the community to modernise and refactor the Adapt Framework using much newer ECMAScript standards.

#### Limitations
* You can **only** use ES6-8 in the `/js/` folder of the core and plugins.
* The `/required/` folder, the `/libraries/` folder and externally required modules **do not** support ES6-8 as these are not transpiled by our build process and will not work in IE11.
* You **should not** use the [`import`](https://exploringjs.com/es6/ch_modules.html) and [`export`](https://exploringjs.com/es6/ch_modules.html) statements as we are still using [requirejs](https://requirejs.org/) as our module bundler.
* If using ES6-8 in a plugin, you **must** specify `"framework": ">=5.3"` in the bower.json.


### ES6 classes and Backbone
There are a few major concepts worth understanding before using [ES6 Classes](https://exploringjs.com/es6/ch_classes.html) and [Backbone](https://backbonejs.org/) together. Backbone is an ES5 library for providing an easy class abstraction and a few base classes from which to extend and make new, easy to read behaviours. ES6 Classes are the standardised ECMAScript native class abstraction. Both Backbone and ES6 Classes seek to provide class abstractions in similar but subtly different ways.

#### ECMAScript Class origins
A class in ECMAScript is simply a function called using the `new` keyword. This function is called the `constructor` function and is executed as usual using the `()` notation. When we call a constructor function using the `new` keyword, a new object instance is created and passed into the function as its `this` keyword. We call this process instantiation - creating a new instance of the class.
```js
var Class = function() { // constructor function
  this; // is a new instance of the class
};
var instance = new Class(); // instantiation
````
The new keyword allows us to specify a set of behaviours on the class which each new object instance will inherit. These behaviours don't live on the instance directly but are instead inherited from the parent Class.
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
It is possible to create many layers of inheritance such that a class is able to inherit behaviour from another and all behaviour from all classes in the chain of inheritance will be expressed on the instance.
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

The named values on the objects passed into the `Backbone.Class.extend` function are copied property name by property name onto the constructor.prototype and constructor respectively. This means that with Backbone, a getter's return value will be copied rather than the getter property description.

#### Class static properties
Aside from being able to define constructor prototype behaviour for each instance, it is possible to assign properties directly to the class constructor, these are called static properties. Class static properties are often helpful for defining behaviour which belongs to a class abstraction but which is not specific to an instance of the class.
```js
var Class = function Constructor() {
  Class.recordInstances(); // record that a new instance was made
};

Class.instances = 0;
Class.recordInstances = function() {
  this.instances++;
};
```
Contrast [String.fromCharCode()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode) with [String.prototype.charCodeAt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt).

Static properties are defined slightly differently in Backbone and ES6.

Backbone:
```js
var Class = new Backbone.Model.extend({
  // defines the constructor.prototype object properties

  log: function() {}

}, {
  // defines class static properties

  recordInstances: function() {}

});
```
ES6:
```js
class Class {
  
  // define a constructor.prototype object property
  log() {}

  // define a class static property
  static recordInstances() {}

}
```

Natively Backbone and ES6 differ in the way they treat class static properties. Backbone will copy the parent class static property values and assign them to the child class at the same property name, whereas ES6 will inherit parent class static properties on the child class.

In Adapt Framework we have a [polyfill](https://github.com/adaptlearning/adapt_framework/blob/master/src/core/libraries/backbone.es6.js) that corrects the Backbone's static property behaviour and brings it inline with ES6 inheritance, such that parent class static properties are now inherited by the child class in Adapt Framework.

#### Practical differences between ES6 and Backbone classes
##### `Backbone.Class.extend` is by value, not by definition 
When the `extend` function is called from a Backbone class, the extend function copies the values of the enumerable properties by name from both the prototype and static objects. As the `extend` function copies values only it disregards property descriptions. This means that a getter defined for Backbone extend to copy will only copy the getter's value and not the getter definition.
```js
var constructorPrototype = {};
Object.defineProperty(constructorPrototype, 'test', {
  get: function() {
    // perform tasks
    return 1;
  }
});

var Class = new Backbone.Model.extend(constructorPrototype);
```
The above definition would only copy the value of the `test` property to the constructor prototype rather than copying the property definition.

It will produce:
```js
Class.prototype === {
  test: 1
};

var instance = new Class();
// the defined getter function isn't called
instance.test === 1;
```
And not:
```js
Class.prototype === {
  get test: function() {
    // perform tasks
    return 1;
  }
};
```

The way to define a getter or setter on a Backbone class is to perform the `Object.defineProperty` on the `constructor.prototype` after the class creation.

```js
var Class = new Backbone.Model.extend({});
Object.defineProperty(Class.prototype, 'test', {
  get: function() {
    // perform tasks
    return 1;
  }
});
```

##### Default inherited properties
With Backbone classes it is possible to assign any value or reference to the constructor's prototype object or to the class statically and for it to be inherited on the instance. It is however more complicated to add a property getter/setter.
```js
var Class = Backbone.Model.extend({
  a: null,
  b: 1,
  c: "string",
  d: function() {},
  e: {},
  f: []
}, {
  A: null,
  B: 1,
  C: "string",
  D: function() {},
  E: {},
  F: []
});

// prototype getter/setter definition
Object.defineProperty(Class.prototype.g, {
  get: function() {},
  set: function(value) {}
});

// static getter/setter definition
Object.defineProperty(Class.G, {
  get: function() {},
  set: function(value) {}
});

var instance = new Class();
// the value of a is inherited from the class prototype
instance.a === null;
```

In ES6 it is only possible to define a getter, setter or function on both the constructor's prototype object and on the class statically. It is more difficult to assign inherited default values on ES6 classes but much easier to define getters and setters.

```js
class Class {

  d() {}
  get g() {}
  set g(value) {}
 
  static D() {}
  static get G() {}
  static set G(value) {}

}

// assign inheritable defaults
Class.prototype.a = null;
Class.prototype.b = 1;
Class.prototype.c = "string";
Class.prototype.e = {};
Class.prototype.f = [];

// assign static defaults
Class.A = null;
Class.B = 1;
Class.C = "string";
Class.E = {};
Class.F = [];

var instance = new Class();
// the value of a is inherited from the class prototype
instance.a === null;


```

The best way to set custom default values on ES6 classes is to do that in the `constructor`, `preinitialize` or `initialize` functions. These values will not inherited from the constructor prototype but will instead exist on the instance.

```js
class Class {
  preinitialize() {
    this.customDefault = 1;
  }
}
```

##### ES6 constructor vs Backbone initialize
Backbone classes come with predefined constructors which provide default class instantiation behaviours. The `Backbone.Model` class has a constructor which initializes model defaults, `Backbone.View` has behaviour which constructs the parent element attached to the view instance at `this.$el`. It is possible to override the constructor function in both ES6 and Backbone classes as follows.

Backbone:
```js
var Class = Backbone.View.extend({
  constructor: function() {}
});
```

ES6:
```js
class Class {
  constructor() {}
}
```

It is very unlikely however that anyone would want to override the default constructor behaviour of Backbone classes and so the Backbone constructor functions call a series of functions from which the default constructor can be extended rather than being overridden.

```js
var Class = Backbone.View.extend({
  preinitialize: function() {
    // executed before default constructor behaviour
  },
  initialize: function() {
    // executed after default constructor behaviour
  }
});
```

The same pattern continues to apply when using ES6 syntax.

```js
class Class extends Backbone.View {
  preinitialize() {
   // executed before default constructor behaviour
  }
  initialize() {
   // executed after default constructor behaviour
  }
}
```

##### Backbone initializing properties: defaults, id, attributes, className
As `Backbone.extend` doesn't copy property definitions and as ES6 classes cannot have easily defined default values, it is easiest to convert all Backbone initializing properties to their alternative syntax, as function definitions.

```js
var Class = Backbone.Model.extend({
  defaults: {
    // defaults definition
  }
});

var Class = Backbone.View.extend({
  attributes: {
    // defaults definition
  }
});
```

The above code would be translated into the following in ES6.

```js
class Class extends Backbone.Model {
   defaults() {
     return {
       // defaults definition
     };
   }
}

class Class extends Backbone.View {
   attributes() {
     return {
       // defaults definition
     };
   }
}
```

##### Super
Previously if we needed to call a parent class function from the child class which has been overridden, we would need a reference to the parent class.
```js
var Class = Backbone.Model.extend({

  test: function() {
    console.log('parent');
  }

});

var Class1 = Class.extend({

  initialize: function() {
    this.test();
  },

  test: function() {
    // Call the test function on the parent class
    Class.prototype.test.apply(this, arguments);
    console.log('parent');
  }

});
```

In ES6 it becomes easier to do this with the `super` keyword.
```js
class Class extends Backbone.Model {

  test() {
    console.log('parent');
  }

}

class Class1 extends Class {

  initialize() {
    this.test();
  }

  test(...args) {
    // Call the test function on the parent class
    super.test(...args);
    console.log('child');
  }

}
```

### End
Happy coding!
