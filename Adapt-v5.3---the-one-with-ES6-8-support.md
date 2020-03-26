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