# Yield

`yield` is a variable that holds the rendered contents of the current page. When visiting `/blog`, the rendered contents of `blog/index.ejs` (or `.md`/`.jade`) become available as `yield` inside the wrapping layout.

## Why?

When using [Layouts](layout) and [Partials](partial), you’ll want to control where the wrapped page’s content appears. That content is contained in the `yield` variable, which you can place anywhere in your layout template.

## Usage

`yield` is available as a variable inside `_layout.ejs` (or `_layout.jade`), and inside any explicit layout set via `_data.json` ([covered in Layouts](layout)). It is **not** available inside the page being wrapped — only inside the layout (or a partial called from the layout).

## EJS Example

Given the following directory structure:

```
mysite/
  |- _layout.ejs
  |- index.ejs
  `- about.md
```

When visiting `/about`, the content from `about.md` needs to be shown. Visiting `/`, similarly, needs to show the content from `index.ejs`. Both pages are wrapped by `_layout.ejs`.

In `_layout.ejs`, the `yield` variable indicates where the page content goes:

```ejs
<!DOCTYPE html>
<html>
  <head>
    <title>Example</title>
  </head>
  <body>
    <%- yield %>
  </body>
</html>
```

The `<%- yield %>` tag (with the dash) outputs the page content **unescaped**. Using `<%= yield %>` instead would HTML-escape the content, producing visible markup tags on the page. This is the most common Harp bug — always use the dash for `yield` and `partial(...)`.

To move where the content appears, just move the `yield` variable:

```ejs
<!DOCTYPE html>
<html>
  <head>
    <title>Example</title>
  </head>
  <body>
    <article>
      <h1>Hello, world</h1>
      <section>
        <%- yield %>
      </section>
    </article>
  </body>
</html>
```

## Jade Example

The same project, with Jade:

```
mysite/
  |- _layout.jade
  |- index.jade
  `- about.md
```

In `_layout.jade`:

```jade
doctype html
html
  head
    title Example
  body
    != yield
```

The `!=` (instead of `=`) tells Jade not to HTML-escape the output — same idea as the EJS dash. Move `yield` wherever you want the content to appear.

## Also see

- [Layouts](layout)
- [EJS](ejs)
- [Jade](jade)
