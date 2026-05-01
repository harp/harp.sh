# The `current` object

The `current` object is the best way to apply active state to your application’s navigation. It’s available in every template and describes the page being rendered right now.

## Why?

When reusing templates for things like navigation, the `current` object lets you apply an active state to the right link, conditionally render layouts or partials, or otherwise branch on which page is loading — all without writing a new copy of the template per page.

## Properties

- **path** *(Array)* — the file path of the current page, split on `/`, with file extensions stripped.
- **source** *(String)* — the last element of `path`.

For most files, the extension is dropped from `source`. The one exception: explicit double-extension files (e.g., `feed.json.ejs`) keep the inner extension, so `current.source` is `"feed.json"` for that file.

Harp updates `current` on every request.

For example, visiting `/articles/hello-world` produces:

```json
{
  "path": ["articles", "hello-world"],
  "source": "hello-world"
}
```

Visiting `/articles/` produces:

```json
{
  "path": ["articles", "index"],
  "source": "index"
}
```

Visiting `/feed.json` (rendered from `feed.json.ejs`) produces:

```json
{
  "path": ["feed.json"],
  "source": "feed.json"
}
```

## Example: active nav state

This application has an `index.ejs`, an `about.ejs`, and an `articles/` section. All three pages reuse a `_nav.ejs` partial:

```
mysite/
  |- _nav.ejs
  |- index.ejs
  |- about.ejs
  `- articles/
      |- _data.json
      |- index.ejs
      `- hello-world.md
```

### EJS

`_nav.ejs`, using `current.source` and `current.path` to set an `active` class on the right link:

```ejs
<ul>
  <li class="<%= current.path.length === 1 && current.source === 'index' ? 'active' : '' %>">
    <a href="/">Home</a>
  </li>
  <li class="<%= current.source === 'about' ? 'active' : '' %>">
    <a href="/about">About</a>
  </li>
  <li class="<%= current.path[0] === 'articles' ? 'active' : '' %>">
    <a href="/articles">Articles</a>
  </li>
</ul>
```

A couple of patterns worth noting:

- **Home link.** Both the path length **and** source check are needed. Visiting `/articles/` also has `current.source === 'index'` (it’s `articles/index.ejs`), so checking `source` alone would mark Home as active when you’re on the articles index.
- **Section link.** Checking `current.path[0]` matches both `/articles/` and any nested page like `/articles/hello-world` — useful for highlighting the section regardless of which sub-page is active.

### Jade

Same idea with Jade:

```jade
ul
  li(class=current.path.length === 1 && current.source === 'index' ? 'active' : '')
    a(href="/") Home
  li(class=current.source === 'about' ? 'active' : '')
    a(href="/about") About
  li(class=current.path[0] === 'articles' ? 'active' : '')
    a(href="/articles") Articles
```

The `class` attribute can be styled with CSS, [Sass](sass), [LESS](less), or [Stylus](stylus).
