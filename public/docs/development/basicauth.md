# Basic Authentication

Add a password to your site to restrict who can visit it.

## Why?

You may want an efficient way to add password protection to an entire static site or client-side application — whether it’s for internal use, a staging preview, or a temporary measure while you work on a project with a client.

## Example

![Logging into a Harp application with basic authentication.](../images/basic-auth-1.gif)

Create a `_harp.json` file in your served directory (or `harp.json` if you’re using the legacy app-style with a `public/` subdirectory). The following password-protects your application with the username `Ali Baba` and password `Open, Sesame!`:

```json
{
  "basicAuth": "Ali Baba:Open, Sesame!"
}
```

## Multiple accounts

You can also specify multiple accounts as an array:

```json
{
  "basicAuth": ["user1:pass1", "user2:pass2", "user3:pass3"]
}
```

## The full `_harp.json` file

`basicAuth` is a top-level key in `_harp.json`, sitting alongside [any other properties](globals). It’s **not** nested under `globals`. A longer config combining the two:

```json
{
  "basicAuth": "Ali Baba:Open, Sesame!",
  "globals": {
    "title": "Ali Baba’s blog",
    "author": "Ali Baba",
    "description": "A secret blog"
  }
}
```

## Disabling auth

To leave the `basicAuth` property in the file but turn off enforcement, set it to an empty array:

```json
{
  "basicAuth": []
}
```

## Basic Authentication and compiled output

Basic Auth is a runtime feature of Harp’s web server. When you compile your project to static files (`harp <source> <build>`) and serve that compiled output from another host — nginx, S3, GitHub Pages, Cloudflare Pages, etc. — Harp is no longer in the request path, so `basicAuth` has no effect. The compiled HTML, CSS, and JavaScript is delivered directly by the new host.

If you need password protection on a static deployment, configure it at the host level (most CDNs and static hosts support some form of password gating). To keep using Harp’s built-in `basicAuth`, run Harp itself as the web server in production — for example, on a [Heroku](/docs/deployment/heroku) dyno or your own VPS.
