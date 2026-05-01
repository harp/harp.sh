# Layouts

A Layout is a common template that includes all content except for one main content area. You can think of a Layout as the inverse of a `partial`.

* [Creating Layouts with EJS](#ejs)
* [Creating Layouts with Jade](#jade)
* [Multiple Layouts](#multiple-layouts)
* [Explicit Layouts](#explicit-layouts)
* [Opting out of a Layout](#no-layout)
* [Nested Layouts](#nested-layout)

## Why?

Most sites have common headers, footers, and navigation that should appear on every page. A Layout lets you define that chrome once and have Harp wrap each page with it automatically.

## Usage

A Layout is a template file named `_layout.ejs` (or `_layout.jade`) placed in the directory whose pages it should wrap. Inside it, [a `yield` variable](yield) marks where the page content gets inserted.

<h2 id="ejs">Example using EJS</h2>

Given a project with this structure:

```
mysite/
  |- _layout.ejs
  `- index.ejs
```

**`_layout.ejs`**:

```ejs
<!DOCTYPE html>
<html>
  <head>
    <title>My Site</title>
  </head>
  <body>
    <%- yield %>
    <footer>
      <p>Copyright © foobar</p>
    </footer>
  </body>
</html>
```

The `<%- yield %>` tag (note the dash) outputs the wrapped page content unescaped. Using `<%= yield %>` instead would HTML-escape the content, producing visible markup tags on the page. The same dash rule applies to `<%- partial(...) %>`.

**`index.ejs`**:

```ejs
<h1>My Site</h1>
<p>Welcome to my very first site.</p>
```

Final result:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Site</title>
  </head>
  <body>
    <h1>My Site</h1>
    <p>Welcome to my very first site.</p>
    <footer>
      <p>Copyright © foobar</p>
    </footer>
  </body>
</html>
```

<h2 id="jade">Example using Jade</h2>

Layouts can also be `.jade` files, and you can mix and match: a `_layout.jade` can wrap an `index.ejs` page, or vice versa.

```
mysite/
  |- _layout.jade
  `- index.jade
```

**`_layout.jade`**:

```jade
doctype html
html
  head
    title My Site
  body
    != yield
    footer
      p Copyright © foobar
```

In Jade, `!= yield` (instead of `= yield`) tells the template engine not to HTML-escape — same idea as the `<%- %>` dash in EJS.

**`index.jade`**:

```jade
h1 My Site
p Welcome to my very first site.
```

<h2 id="multiple-layouts">Multiple Layouts</h2>

Subdirectories can have their own `_layout` files that override the parent layout for pages inside that subtree. In the following example, the articles directory uses its own layout:

```
mysite/
  |- _layout.ejs
  |- index.ejs
  |- about.md
  `- articles/
      |- _layout.ejs
      |- article-one.md
      `- article-two.md
```

`index.ejs` and `about.md` use the root `_layout.ejs`. Anything in `articles/` — `article-one.md` and `article-two.md` — uses the `_layout.ejs` in that subdirectory instead.

<h2 id="explicit-layouts">Explicit Layouts</h2>

Layouts other than `_layout` can be specified per-page in a `_data.json` entry. This is useful for finer control or non-standard naming.

```
mysite/
  |- _layout.ejs
  |- index.ejs
  `- articles/
      |- _data.json
      |- _featured-layout.ejs
      |- _another-layout.ejs
      |- article-one.md
      `- article-two.md
```

In `articles/_data.json`:

```json
{
  "article-one": {
    "layout": "_featured-layout",
    "title": "Example Title"
  },
  "article-two": {
    "layout": "_another-layout",
    "title": "Another Example Title"
  }
}
```

Each article uses its specified layout. The `layout` value is a path **without** the file extension. Path resolution:

- Relative to the page’s own directory first. `"layout": "_featured-layout"` looks for `articles/_featured-layout.*`.
- Falls back to the project root if not found locally. `"layout": "../../_layout"` works for explicit parent traversal.

One automatic exemption worth knowing: pages that emit a `.json` extension (e.g., `feed.json.ejs`) skip layouts entirely — useful for API routes and feeds, no `"layout": false` needed.

<h2 id="no-layout">Opting out of a Layout</h2>

To exempt a single page from layout wrapping, set `"layout": false` in `_data.json`:

```
mysite/
  |- _data.json
  |- _layout.ejs
  |- index.ejs
  `- about.md
```

`_data.json`:

```json
{
  "about": {
    "layout": false
  }
}
```

`about.md` renders as plain HTML without the layout. Other pages (like `index.ejs` here) continue to use `_layout.ejs`.

The `layout` key is not inherited by partials, so partials never accidentally get wrapped — only pages do.

<h2 id="nested-layout">Nested Layouts</h2>

Harp doesn’t have a built-in nested-layout mechanism, but `partial()` plus the [`current`](current) object lets you achieve the same thing. For example, `_layout.ejs` might look like this:

```ejs
<!-- If the current page is inside blog/ but isn't blog/index... -->
<% if (current.path[0] === "blog" && current.source !== "index") { %>
  <!-- Wrap the page in a per-section partial -->
  <%- partial(current.path[0] + "/_nest") %>
<% } else { %>
  <%- yield %>
<% } %>
```

Then `blog/_nest.ejs` can wrap the page content with additional chrome, using `<%- yield %>` itself:

```ejs
<article>
  <%- yield %>
</article>
```

Now the `blog/` index renders normally, while individual blog posts (e.g., `blog/hello-world`) get an extra `<article>` wrapper. The `_nest.ejs` file could be named anything; it’s a regular [partial](partial).

If you’re using [Jade](jade), you can also reach for Jade’s native `block` and `extends` features to compose nested layouts.
