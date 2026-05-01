# 404 Not Found status code

Use Harp to show a custom 404 page.

## Why

Whatever you’re making deserves a custom 404 page — somewhere you can give visitors useful information and keep the site’s design consistent.

## Usage

Add a `404.html` file in your served directory. (`404.ejs`, `404.md`, or `404.jade` work too — they’ll compile to HTML.) When a request doesn’t match any file, Harp serves the `404.*` contents with a `404 Not Found` status code.

## Example

The simplest case: drop a `404.html` next to your other pages.

```
mysite/
  |- 404.html
  |- index.html
  `- main.less
```

If you’d like the 404 page to share your site’s layout, use a compilable extension (`.md`, `.ejs`, or `.jade`) so it’s wrapped by `_layout.*`:

```
mysite/
  |- _layout.ejs
  |- 404.md
  |- index.ejs
  `- main.scss
```

The [_layout](layout) file wraps both `index.ejs` and `404.md`.

## Cascading 404 files

`404.*` files cascade up the directory tree. When a request misses, Harp walks up from the request path, and at each directory level checks for a `200.*` first and then a `404.*`. The first match wins.

This means each section of your site can have its own 404 page:

```
mysite/
  |- 404.html                  <-- top-level 404
  |- index.html
  `- shop/
      |- 404.ejs               <-- shop-specific 404
      |- index.ejs
      `- products/
          `- widget.md
```

A request like `/shop/missing-product` matches `shop/404.ejs` (deeper directory wins). A request like `/about` (not present) walks up and is served the top-level `404.html`. If neither file existed, Harp would fall back to a generic 404 response.

> A `200.*` and a `404.*` in the same directory: the `200.*` wins. If you’re routing a client-side app under `/shop/` with a `200.ejs`, your `404.ejs` in the same directory is unreachable.

## Compile output

When you run `harp <source> <build>`, `404.*` files are emitted as `404.html` in the corresponding output directory. Most static hosts (Netlify, Vercel, GitHub Pages, Cloudflare Pages) recognize a top-level `404.html` and use it for unmatched URLs automatically.
