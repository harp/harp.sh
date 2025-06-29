# How to create _art directed_ blog posts with Harp

This recipie will show you how to style individual posts differently.

## Overview

Art directed blog posts commonly refer to styling blog posts or portfolio projects distinctly, depending on the content included.

## Example using Jade templating

You might structure your site as follows:

```
▾ /
  ▪ _layout.jade         <-- Basic layout will wrap everything
  ▪ index.jade           <-- Index page
  ▪ 404.jade             <-- Your 404 page, will get served at /404
  ▪ about.md             <-- Your about page, will get served at /about
  ▪ css/
      ▪ main.scss        <-- Main Sass file
  ▪ blog/
      ▪ _data.json       <-- Your blog’s flexible metadata
      ▪ index.jade       <-- Blog index
      ▪ post-1.md        <-- An example post
      …
      ▪ post-6.md        <-- Another blog item
      ▪ post-7.jade      <-- A blog post where you want more control over the markup, so used Jade
```

Now, for the art directed posts, you can use [Harp’s `current` variable](https://harp.sh/docs/development/current). You can use it in the `_layout` file, like this:

```jade
doctype
html(class="#{ current.path[0] == 'blog' ? current.source : '' }")
  head
    title Hello, world
  body
    != yield
```

When you visit `portfolio/project-6`, This will render as:

```html
<!DOCTYPE html>
  <html class="project-6">
    <head>
      …
```

…allowing you to style the post differently. When you visit other pages, it will just render without a class name. You could change this however you want, and just have the page’s class name everywhere if you decided that was appropriate for your used case. Another example might be to prefix the class name with `art-dir-` or something.

## Example using EJS templating

You might structure your site as follows:

```
▾ /
  ▪ _layout.ejs          <-- Basic layout will wrap everything
  ▪ index.ejs            <-- Index page
  ▪ 404.ejs              <-- Your 404 page, will get served at /404
  ▪ about.md             <-- Your about page, will get served at /about
  ▪ css/
      ▪ main.scss        <-- Main Sass file
  ▪ blog/
      ▪ _data.json       <-- Your blog’s flexible metadata
      ▪ index.ejs        <-- Blog index
      ▪ post-1.md        <-- An example post
      …
      ▪ post-6.md        <-- Another blog item
      ▪ post-7.ejs       <-- A blog post where you want more control over the markup, so used EJS
```

Now, for the art directed posts, you can use [Harp’s `current` variable](https://harp.sh/docs/development/current). You can use it in the `_layout` file, like this:

```ejs
<!DOCTYPE html>
<html class="<%= current.path[0] == 'blog' ? current.source : '' %>">
  <head>
    <title>Hello, world</title>
  </head>
  <body>
    <%- yield %>
  </body>
</html>
```

When you visit `portfolio/project-6`, This will render as:

```html
<!DOCTYPE html>
<html class="project-6">
  <head>
    …
```

…allowing you to style the post differently. When you visit other pages, it will just render without a class name. You could change this however you want, and just have the page’s class name everywhere if you decided that was appropriate for your used case. Another example might be to prefix the class name with `art-dir-` or something.

## Also see

- [Build a static blog with Harp, which contains some basics](http://kennethormandy.com/journal/start-a-blog-with-harp)
- [Templating with EJS](../docs/development/ejs)
- [Templating with Jade](../docs/development/jade)
