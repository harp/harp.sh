# Contents

The `_contents` array gives you a list of files in a directory. It’s useful when you want to iterate over files without maintaining metadata for each one.

## Why?

Sometimes you have a directory of files — images, downloads, fonts — and want to render a list of them without manually keeping a `_data.json` entry per file. `_contents` gives you that listing automatically, generated from the filesystem.

## Shape

`_contents` is an **array of filename strings**. It includes the servable files in that exact directory and excludes:

- Files and directories whose names start with `_` (the underscore convention for layouts, partials, and metadata).
- Files starting with `.` (hidden files like `.DS_Store`).
- Subdirectories themselves — only files in the directory are included, never nested directories or their contents.

You access `_contents` through the `public` namespace, like other directory metadata: `public.images._contents`.

## Example

A directory of images:

```
mysite/
  |- index.ejs
  `- images/
      |- hello-world.jpg
      |- hello-saturn.jpg
      `- hello-jupiter.jpg
```

### EJS

Inside `index.ejs`, iterate over `public.images._contents`:

```ejs
<% public.images._contents.forEach(function(file) { %>
  <% if (/\.(jpg|jpeg|png|gif|webp)$/i.test(file)) { %>
    <img src="/images/<%= file %>" alt="" />
  <% } %>
<% }) %>
```

Result:

```html
<img src="/images/hello-world.jpg" alt="" />
<img src="/images/hello-saturn.jpg" alt="" />
<img src="/images/hello-jupiter.jpg" alt="" />
```

The regex filter matches image extensions; without it, `_contents` would also include any non-image files in the directory.

### Jade

```jade
for file in public.images._contents
  img(src="/images/#{ file }")
```

## Other use cases

`_contents` works for any directory of files. Common patterns:

- A downloads page listing every file in `downloads/`.
- A list of fonts, audio clips, or PDFs.
- A "recent posts" list keyed off filename — though [`_data.json`](metadata) is preferred when you have a title, date, or author to attach.

## Also see

- [Metadata](metadata) — when you need structured data (title, date, etc.) for each file, reach for `_data.json` instead of `_contents`.
