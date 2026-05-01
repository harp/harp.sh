# Partials

Partials are first-class in Harp and work the same way across EJS and Jade. A partial can be included anywhere in an [EJS](ejs) or [Jade](jade) file, and the rendered contents get mixed in.

* [Using partials](#use)
* [Using partials in an `.ejs` file](#ejs)
* [Using partials in a `.jade` file](#jade)
* [On Markdown and the `partial` function](#markdown)

## Why?

To keep your app DRY, you need a way to reuse content. Partials provide a simple interface for great flexibility around reusing pieces of your project — headers, footers, navs, cards, anything that appears in more than one place.

## Properties

The `partial` function takes two arguments:

- **path** *(String, required)* — the relative path to the file to include, without the file extension.
- **data** *(Object, optional)* — variables to mix into the partial.

<h2 id="use">Using Partials</h2>

Say you’re making a small website with an `index.ejs` file and an `about.ejs` file, and you want to include a header that repeats on every page. Put the header content in a file named `_header.ejs` and include it from both pages.

Because `_header.ejs`’s name begins with an underscore, it isn’t served directly. Instead, it’s included via the `partial` function.

The `_header.ejs` file can be as simple or complex as you’d like, for example:

```ejs
<h1>This is my site</h1>
<p>This content is in a partial.</p>
```

<h2 id="ejs">Using partials in an EJS file</h2>

Inside `index.ejs`, call `partial("_header")` to include the content of `_header.ejs`:

```ejs
<%- partial("_header") %>
```

Note the `<%- %>` tags (with the dash) — these output the partial unescaped, which is what you want for HTML. Using `<%= %>` (no dash) would HTML-escape the partial’s output, producing visible markup tags on the page. The same rule applies to `yield` inside layouts.

Now Harp will render `index.ejs` with the content from `_header.ejs`. You could repeat this for `about.ejs`, but what if the header should change between the two pages?

Update `_header.ejs` so the `<h1>` contains a `title` variable:

```ejs
<h1><%= title %></h1>
<p>This content is in a partial.</p>
```

Then pass in the `title` when you call the partial:

```ejs
<%- partial("_header", { title: "About me" }) %>
```

`title` is an arbitrary name — call it whatever fits the context. Multiple variables work too:

```ejs
<%- partial("_header", { title: "About me", description: "This is my about page" }) %>
```

<h2 id="jade">Using Partials in a Jade file</h2>

Using partials in Jade is very similar to EJS. Functions in Jade are prefixed with `!= ` rather than wrapped in `<%- %>`. Both forms render the partial unescaped:

```jade
!= partial("_header")
```

Jade may import EJS partials and vice versa. To pass data:

```jade
!= partial("_header", { title: "Contact me" })
```

Multiple values:

```jade
!= partial("_header", { title: "Contact me", description: "This is my Jade contact page with an EJS header" })
```

If you’d like to set fallbacks for your variables — in case you don’t pass any data into the partial — you can do this by setting [global variables](globals).

<h2 id="markdown">On Markdown and the `partial` function</h2>

You **cannot** call `partial()` from inside a `.md` file. The reason is structural: Markdown files are compiled to static HTML by [`marked`](https://marked.js.org/), which is a Markdown renderer, not a template engine. It doesn’t execute template code, so functions like `partial()` (and EJS-style interpolation more generally) aren’t available inside a `.md` body. EJS and Jade *are* template engines and do execute template code, which is why these features work there.

What you *can* do:

**Include a Markdown file as a partial from EJS or Jade.** This works just like any other partial; the Markdown gets rendered to HTML and dropped in. With a `_shared/an-example.md` file:

```ejs
<article><%- partial("_shared/an-example") %></article>
```

```jade
article!= partial("_shared/an-example")
```

**Use the layout to add chrome around the markdown.** A `.md` page is wrapped by the nearest `_layout.ejs`, which runs as a normal EJS template — so all the variables, partials, and template logic you need can live in the layout. The body of the `.md` file stays pure prose.

If you genuinely need a partial inside the body of a content page, convert that page from `.md` to `.ejs`.
