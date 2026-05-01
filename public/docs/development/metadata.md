# Metadata

Metadata is scoped data injected into specific pages through the `_data.json` file.

## Why?

Sometimes you want to separate concerns, or keeping all your data in a single global file isn’t advantageous. File metadata is perfect for this — it lets each directory carry its own variables, available only to the templates inside that directory.

## Example

```
mysite/
  ├ _harp.json              <-- site-wide globals (optional)
  ├ index.ejs
  └ articles/
      ├ _data.json          <-- per-directory metadata for articles
      ├ hello-world.md      <-- hello world article
      └ hello-brazil.md     <-- hello brazil article
```

Your application can have several `_data.json` files, each in its own directory. You can also place a `_data.json` in the root of the served directory to set metadata for pages there.

A `_data.json` file may contain the following:

```json
{
  "hello-world": {
    "title": "Hello World",
    "date": "2026-02-28"
  },
  "hello-brazil": {
    "title": "Hello Brazil",
    "date": "2026-03-04"
  }
}
```

Each top-level key matches a filename in the same directory (without the extension). The variables under that key become plain locals inside the matching template. Inside `articles/hello-world.ejs`, `<%= title %>` resolves to `"Hello World"`. The same works in `.jade`.

> Don’t include the file extension in your `_data.json` keys. `"hello-world.md": { ... }` will throw an error.

### Markdown pages

A `.md` file’s matching `_data.json` entry is attached to its render context too, but the markdown processor itself doesn’t substitute variables — `<%= title %>` inside a `.md` body just appears as literal text. The values *are* available to the wrapping `_layout.ejs` and to any other template via `public.articles._data`, which is the usual way you’d use them: setting the `<title>` tag, choosing a layout, or rendering an index page that enumerates the entries.

## Accessing the whole map

The whole `_data.json` object is also available globally as `public.articles._data`. The `public` namespace always wraps your served-root data tree, regardless of whether your project has a literal `public/` directory. Individual entries are reachable as `public.articles._data["hello-world"]`.

This is how an index page enumerates the entries. In EJS:

```ejs
<% for (var slug in public.articles._data) { %>
  <% var article = public.articles._data[slug] %>
  <a href="/articles/<%= slug %>">
    <h2><%= article.title %></h2>
  </a>
<% } %>
```

In Jade:

```jade
for article, slug in public.articles._data
  a(href="/articles/#{ slug }")
    h2= article.title
```

## Precedence

When the same variable name is set in more than one place, Harp resolves it from highest priority to lowest:

1. **Data passed explicitly to `partial(name, { ... })`** — wins over everything else inside that partial.
2. **The page's own `_data.json` entry** — overrides globals for that page.
3. **Globals from `_harp.json`** — the fallback.

For example, you can set a `title` global in `_harp.json` for the whole site, then override it on individual pages by adding a `title` to the matching `_data.json` entry. (See the [custom title recipe](../../recipes/custom-title-description) for a worked example.)

## Special keys

Most keys in `_data.json` are passthrough — whatever you set becomes a template local. One key is special:

- `layout` — set to `false` to skip layout wrapping for that page, or to a string path to use an alternate layout. See [Layout](layout) for details. The `layout` key is **not** inherited by partials, so partials never accidentally get wrapped.

## Also see

- [Globals](globals) — site-wide values defined in `_harp.json`
- [Layout](layout) — controlling page wrapping with the `layout` key
- [Add a Custom Title and Description per page](../../recipes/custom-title-description)
- [A quick example Harp app that uses the correct title for your blog](https://gist.github.com/kennethormandy/6834709)
