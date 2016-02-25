# Routes

In the [previous tutorial](./init.md), we set up a boilerplate application with
a basic directory structure. We're going to talk about modularized routing using
express routers.

In your `routes/` directory, create a new file called `index.js`. This is where
we're going to organize our api routes.

```js
'use strict';

import express from 'express';

const { Router } = express; // remember destructuring?
const api = new Router();



export default api;

```

Express provides a way of creating a stripped down express app, which doesn't
have methods like `.listen()` and other server starting things. An express
router does let you set up api endpoints. You have access to all of the methods
like `.use()`, `.get()`, `.post()`, and all the other middleware mounting
methods. The router itself is middleware that you mount onto your app or other
routers.

The empty space between the `const api` and `export default` lines is for you
to fill in with with your routes.

Since this is a todo app, let's create a new file called `todos.js` in the
`routes/` directory and start it out with this content:

```js
'use strict';

import express from 'express';

const { Router } = express;
const todosRouter = new Router();

const todos = [];

app.get('/', (req, res, next) => {
  res.json(todos);
});

export default todosRouter;
```

This is a simple router that has one route: `/`. When you make a `GET` request
to that route, it returns a json response with the value of todos.

Let's go back to our `routes/index.js` and add the following:

```js
'use strict';

import express from 'express';
import todos from './todos'; // Import our todosRouter

const { Router } = express;
const api = new Router();

api.use('/todos', todos); // Mount the todosRouter to the route /todos

export default api;

```

Now
