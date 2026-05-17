# Embedded `express` Middleware

Sometimes you already have a server, but you want to use Harp as your asset pipeline, getting the benefits of Harp’s preprocessing.

This example combines the power of express with all the benefits of Harp, in one project. No external preprocessing, no complicated configuration, and no client-side parsers; just coding bliss. Best of all, setup is extremely easy.

1. ### Add Harp as a dependency

  Include Harp as a dependency in the `package.json` file of your Express app.

  ```json
  {
    "name": "myapp",
    "version": "0.1.0",
    "dependencies": {
      "express": "3.x",
      "harp": "*"
    }
  }
  ```

2. ### Use `harp.mount`

  Next, you’ll use `harp.mount` just like you would the static middleware.

  ```javascript
  var express = require("express");
  var harp = require("harp");
  var app = express();

  app.use(express.static(__dirname + "/public"));
  app.use(harp.mount(__dirname + "/public"));

  app.listen(9000);

  // routes as normal
  ```

3. ### Add your Harp app

  All done! Now you put your Harp app’s assets in the `public` directory. Here’s an example of what your `public` directory might look like:

  ```
  /public
    /_data.json
    /_harp.json
    /index.ejs
  ```

You can [pass data to your template](/docs/development/metadata) the same way you do with a normal Harp app. For example, using `_data.json`:

```json
{
  "index": {
    "title": "Hello World"
  }
}
```

For global variables, use the `_harp.json` file, like this:

```json
{
  "globals": {
    "foo": "bar"
  }
}
```

Then you can use the `title` and `foo` variables in your `index.ejs` template like this:

```ejs
<h1><%= title %></h1>
<p><%= foo %></p>
```

And that should output this:

```html
<h1>Hello World</h1>
<p>bar</p>
```

## Subtle difference with Harp server

Mounting Harp as a library using `harp.mount()` does not load all the layers of middleware that a regular Harp server (using `harp.server()`) does.

However, `harp.middleware` conveniently exposes all available Harp middleware such as `fallback`, `notFound` and `underscore` so you can easily add additional Harp features to your server in a way that makes sense for your application.

For example:

```javascript
var express = require("express");
var harp = require("harp");
var app = express();
var appRoot = __dirname + "/public";

// Ignore files that start with underscores
app.use(harp.middleware.underscore);

// Serve static assets
app.use(express.static(appRoot));

// Let harp serve application
app.use(harp.mount(appRoot));

// Let 200.jade catch all other requests
app.use(harp.middleware.fallback);

app.listen(9000);
```
