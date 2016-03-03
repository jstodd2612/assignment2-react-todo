# React

There are a soooo many convoluted examples of how to do react including complex
build process and tools. All of that baggage and leave people who are learning
react with a sour taste in their mouths.

For this tutorial, we're going to stick to one file. A simple html file with all
of our libraries loaded via a cdn so we don't have to worry about build
processes. This setup is not ideal for production as load times for large
complex apps will be unacceptable. It is also outdated and will no longer be
supported. We will do it the right way, but right now it's more important that
you learn the concepts of React.

Create a new folder called `public/`, and place a new file called `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>React Todo App</title>
    <script src="https://fb.me/react-0.14.7.min.js"></script>
    <script src="https://fb.me/react-dom-0.14.7.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      ReactDOM.render(
        <h1>Hello World</h1>,
        document.getElementById('root')
      );
    </script>
  </body>
</html>
```

Now open up that `index.html` file in the browser.

Let's take a look at this piece by piece:

- We include 3 difference libraries:
  - **react** - The react library
  - **react-dom** - The react dom library that renders react components to
    the browser DOM. React, by itself, is not tied to the browser, so they split
    out the DOM specific pieces into it's own library.
  - **babel-core/browser** - This is the babel renderer that will transform es6
    and jsx into browser compatible javascript. Note that this library is
    deprecated. We're only using it for quick prototyping and understanding the
    concepts of React

- We have a script tag in the body.

  Note that the `type` attribute is set to `text/babel`. This is only needed
  because of how we're transpiling es6 to es5 in the browser directly. When we
  set up a normal build process, we will not need to worry about this piece.

- Everything in that `<script>` tag can be written in es6 and
  jsx.

- `ReactDOM.render()` takes in two arguments:
  1. A React element. It can have nested elements, but you must only have one
    root element
  2. A DOM element to mount your React component to. You just use the built in
    browser methods like `document.getElementById`. Just make sure you have an
    element on the page with the given id.

# JSX

Before we go any deeper, we should explain `JSX`. [Here's][jsx] a good primer on
what `JSX` is. We'll summarize:

> JSX is a JavaScript syntax extension that looks similar to XML.

```js
var myDivElement = <div className="foo" />;
ReactDOM.render(myDivElement, document.getElementById('example'));
```

When used with React and a transpiler (like babel), it turns JSX into
Javascript. The previous example would be turned into the following code:

```js
var myDivElement = React.createElement(
  'div', // This is the type of html element, or it could be a custom component
  { className: 'foo' } // This represents the attributes of the component
);
ReactDOM.render(myDivElement, document.getElementById('example'));
```

It allows you to represent tree-like structures that can be rendered into html.
You can nest elements just like you would in html:

```js
var myForm = (
  <form>
    <label>
      First Name:
      <input type="text" />
    </label>
    <label>
      Last Name:
      <input type="text" />
    </label>
  </form>
);

ReactDOM.render(myForm, document.getElementById('example'));
```

The previous example gets turned into this:

```js
var myForm = React.createElement('form', null,
  React.createElement('label', null,
    'First Name:',
    React.createElement('input', { type: 'text' })
  ),
  React.createElement('label', null,
    'Last Name:',
    React.createElement('input', { type: 'text' })
  )
);
ReactDOM.render(myForm, document.getElementById('example'));
```

So you can write react without writing in jsx or needing that extra transpile
step, but it's much more verbose and harder to read. Almost all react tutorials
will favor JSX instead of plain JavaScript.

# React Components

TODO

[jsx]: http://facebook.github.io/react/docs/jsx-in-depth.html
