# REST

`REST` stands for "Representational State Transfer". It's essentially a way to
communicate to a server via HTTP by telling it what action you would like to
take on a resource.

A resource is represented by a url. `http://example.com/users` is a resource.
`http://example.com/users/178489322` is a resource. When you request a resource,
the server responds by sending you data, in any number of formats. When you make
an HTTP request to that endpoint, it may return you a `json` encoded body, or
possibly and `xml` encoded body. Or it may respond with an error.

You can tell the server to do different things to any given resource by using
HTTP verbs. You can tell the server to retrieve a resource, update it, delete
it, or create new resources. The server doesn't just automatically adhere to
whatever request you give it, so you have to conform to what the server allows
you to do.

Some common HTTP verbs are as follows:

* `GET` This tells the server to read data. No data modifications should happen
  in this type of request.

* `POST` This tells the server to create a new resource.

* `PUT` This tells the server to update a resource

* `DELETE` This tells the server to delete a resource

So with any given resource url, you can use different HTTP verbs to tell the
server to do different things. For example:

If I `GET http://example.com/users`, I'm telling the server hosted at
`http://example.com` to fetch me the resource under the name `/users`. If I
change the verb to `POST`, I'm then telling the server that I want to create a
new `/users` resource. If that is successful, it may return some sort of user id
that I can use in subsequent requests. If it returned an id of `123`, I could
request `GET http://example.com/users/123` and it should retrieve the data for
the user resource who's id is `123`.

We've got the start of this from the [previous tutorial](./01_routes.md) in our
`routes/todos.js` file. Let's take another look:

```js
'use strict';

import express from 'express';

const { Router } = express;
const todosRouter = new Router();

const todos = [];

// Here we have a route that gets all of the todos
todosRouter.get('/', (req, res, next) => {
  res.json(todos);
});

export default todosRouter;

```

So if we wanted to add a route that could create a todo, we would want to use
the `POST` HTTP verb. Express allows us to easily intercept requests based on
HTTP verb. Add the following after your `todosRouter.get()` call:

```js
todosRouter.post('/', (req, res, next) => {
  todos.push(req.body);
  res.json(req.body);
});
```

Start your server again, and run the following `curl` command to test out your
new `POST` handler:

```
curl -X POST \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data '{
  "name": "newTodo",
  "completed": false
}' \
http://localhost:8000/api/todos
```

First off, with the code that we've currently set up through this set of
tutorials, it should not print out anything. If you put some console.log
statements in the `todosRouter.post('/')` middleware, you'll find that
`req.body` is undefined. You most certainly sent a request body in that curl
request. Before we get into that, let's explain what this `curl` request is
doing.

This command is making a new HTTP request to `http://localhost:8000/api/todos`
with the `POST` verb, and two heads that specify:

1. The content type of the request body
2. What content type I'm expecting in the response

As mentioned earlier, this is all handled by the server, and it's up to the
server to respect these options.

So the problem with our server is that it is not parsing the request body and
putting the result in `req.body`. So we need to include some robust middleware
that will parse the json body for us.

```sh
npm install --save body-parser
```

`body-parser` is a battle-hardened express middleware module that parses various
forms of request body encoding types, including json, urlencoded, text, and a
few others.

To use it, let's include it in our `app.js`

```js
'use strict';

import express from 'express';
import bodyParser from 'bodyParser';
import api from './routes';

const app = express();
const PORT = process.env.PORT || 8000;

// Here's where the magic happens. Any middleware after this have access to
// `req.body` for those requests that come through as `json` bodies with the
// `Content-Type: application/json` header
app.use(bodyParser.json());
app.use('/api', api);

app.listen(PORT, () => console.log(`Server listening on port ${PORT}`));

```

Now if you restart your app and run the curl request from above again, you get
a response back! Right now you're not doing any validation on the data that
comes into the response. We need to verify that it has the right properties and
that they are the right data types so that we don't save bogus data.

TODO: finish talking about data validation and adding in other rest endpoints.