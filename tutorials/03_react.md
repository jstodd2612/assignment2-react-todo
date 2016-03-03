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
      React.render(
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

-

