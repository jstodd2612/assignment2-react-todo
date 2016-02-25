# Initialization

For this tutorial, we're going to set up some boilerplate code and directory
structure. It's important to make some of these decisions up front so that we
don't flip flop to much after we get going.

## `npm`

First thing's first, let's initialize our `package.json` with `npm init`

```sh
npm init
```

Follow the prompts to generate your `package.json`. Now we're ready to start
installing node modules.

I'm going to first install the babel modules we need to get started with that
on the server-side.

```sh
npm install --save babel-core babel-preset-es2015 babel-polyfill
```

The above installed 3 packages:

* `babel-core` - The core babel runtime. It doesn't make any code
  transformations by default. We need plugins that tie into babel's runtime
  code modification stuff.
* `babel-preset-es2015` - This is a babel preset, which contains many babel
  plugins to makes it so you can use a lot of es6 features now without Node
  providing it to you.
* `babel-polyfill` - This polyfills some of the es6 stuff that don't
  necessarily need to transform syntax. For example: Arrow functions (pre
  Node 4) were not supported with the syntax, but babel transforms Arrow
  functions in a way that make it so it works like the es6 spec. A polyfill
  is used for things like adding a new prototype method to Strings and Arrays,
  or a completely new data type like Promises.

In order for babel to know what presets/plugins to use, we must create an
additional file called `.babelrc`, which will act as our babel config. Put in
the following contents:

```
{
  "presets": ["es2015"]
}
```

Note that we did not need to put `babel-preset-es2015` and instead we just put
`es2015`. When we put a string value into the `presets` array, it automatically
looks for packages that start with `babel-preset-`.

In order to use them now, we need to include them in our files. Create two
files called `app.js` and `init.js`. We'll use `init.js` to put in our babel
bootstrapping code.

```js
'use strict';

require('babel/register'); // This starts up the babel runtime parser
require('babel-polyfill'); // This provides the extra es6 items like Promises and Array methods
require('./app'); // Starts up the app be requiring our `index.js`.
```



