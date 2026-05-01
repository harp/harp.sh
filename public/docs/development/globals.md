# Globals

Globals are JSON data stored in your `_harp.json` file that is available to all pages, templates, partials, and layouts.

## Why?

Harp isn’t just about static assets — pages can be created using dynamic content too. Adding values under the `globals` key makes them natively available in every template, with no namespace prefix and no import.

## Defining globals

Drop a `_harp.json` file into your served directory. The `globals` key contains an object of variables you want available throughout your site:

`_harp.json`

```json
{
  "globals": {
    "title": "Acme Site",
    "name": "John Doe",
    "uri": "http://example.com"
  }
}
```

> **Legacy:** Older Framework-Style projects use `harp.json` at the parent of `public/`. The schema is identical.

## Using globals in templates

The values under `globals` become top-level locals in every template.

### EJS

`index.ejs`

```ejs
<html>
  <head>
    <title><%= title %></title>
  </head>
  <body>
    <h1>Hello <%= name %>!</h1>
  </body>
</html>
```

### Jade

`index.jade`

```jade
html
  head
    title #{ title }
  body
    h1 Hello #{ name }!
```

## Other top-level keys

`_harp.json` is a flat object. `globals` is one of several recognized top-level keys; they sit as siblings, not nested under each other:

| Key | What it does |
|------|--------------|
| `globals` | Site-wide template variables, available as plain locals in every template |
| `basicAuth` | HTTP Basic Auth credentials. See [Basic Authentication](basicauth) |
| Any other key | Preserved and emitted into the compiled `globals.json`; treat as your own config namespace |

A longer config combining `globals` and `basicAuth` looks like this:

```json
{
  "globals": {
    "siteTitle": "Acme",
    "author": "John Doe"
  },
  "basicAuth": ["preview:letmein"]
}
```

## Environment variable substitution

Strings of the form `"$VAR_NAME"` anywhere in `_harp.json` are replaced at load time with the value of `process.env.VAR_NAME`. Useful for secrets and per-environment values that shouldn’t be checked into source control:

```json
{
  "globals": {
    "stripeKey": "$STRIPE_PUBLISHABLE_KEY",
    "apiBase": "$API_BASE"
  }
}
```

Run with the environment variables set:

```bash
STRIPE_PUBLISHABLE_KEY=pk_test_123 API_BASE=https://api.example.com harp ./mysite
```

The substitution happens once at config load; templates see the resolved string values, not the `"$VAR_NAME"` literals. If a referenced variable isn’t set, the value will be `undefined`.

## The runtime `environment` global

In addition to anything you define yourself, Harp automatically injects an `environment` global, set to the value of `NODE_ENV` (or `"development"` if unset). Use it to switch behavior between development and production builds:

```ejs
<% if (environment === "production") { %>
  <script src="/analytics.js"></script>
<% } %>
```

See [Environment](environment) for the full story on the runtime environment variable.
