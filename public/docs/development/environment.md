# Environment

The Harp web server can run both locally and in production mode. The `environment` variable is a template global that resolves to `"production"` or `"development"` depending on the current context.

## Why

The Harp web server can run locally for developing, or in production mode as a production-ready web server. With the `environment` variable, your Harp app can behave differently depending on which mode it’s running in.

This is perfect for creating draft posts in a static blog, for example, or loading development-only resources while building a client-side application.

## Use

The value of `environment` is determined at runtime:

* When running `harp <source>` to serve, `environment` is `"development"` unless you set `NODE_ENV=production`.
* When running `harp <source> <build>` to compile, `environment` defaults to `"production"` — so anything gated on production behaviour will still occur in your compiled static output. You can override this by explicitly setting `NODE_ENV=development` before the compile command.

The `environment` value is also exposed as `globals.environment`, in case you’d rather access it through the globals namespace.

## EJS Example

This is a very simple example showing how to use a conditional to check which environment Harp is running in, in EJS.

```ejs
<h1>Harp is in <%- environment %> mode.</h1>
<% if(environment == "production") { %>
  <p>See? Harp is in production mode.</p>
<% } else { %>
  <p>Okay, Harp is in development mode right now.</p>
<% } %>
```

## Jade Example

This is a simple example showing how to use a conditional to check which environment Harp is running in, in Jade.

```jade
h1 Harp is in #{ environment }
if environment == "production"
  p See? Harp is in production mode.
else
 p Okay, Harp is in development mode right now.
```

## Also see

* [CLI](../environment/cli) — full reference for `harp <source>`, `harp <source> <build>`, and the `NODE_ENV=production` flag
* A blog post about [creating Static draft posts with Harp](http://kennethormandy.com/journal/static-draft-posts-with-harp) using the `environment` variable.
