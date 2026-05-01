# Markdown

Markdown’s easy-to-write, easy-to-read format is useful and popular for writing on the web.

## Why?

Harp includes the common, useful preprocessors by default. This means you don’t have to waste time converting your Markdown into HTML — everything just works. Plus, [Jade](jade) and [EJS](ejs) files can import Markdown files as [partials](partial#markdown), allowing you to effectively re-use your writing.

## Usage

Harp’s asset pipeline is easy to use. All preprocessing happens implicitly, so there is nothing to set up. Just name your file with an `.md` extension, and the Harp web server will serve it as `.html`.

Some implementations of Markdown also accept `.markdown`, `.mdown`, or `.txt` extensions. Harp only preprocesses `.md` files.

## Example

This project contains an `index.md` and an `about.md` in the served directory.

```
mysite/
  |- index.md
  `- about.md
```

Both `index.md` and `about.md` are served as HTML. Requests to the following paths will all work:

- `/`
- `/index`
- `/index.html`
- `/about`
- `/about.html`

Compiling the project (`harp ./mysite ./www`) will export the same pages as `index.html` and `about.html` to the build directory.

### GitHub Flavoured Markdown

Harp supports the supplementary [GitHub Flavoured Markdown](https://help.github.com/articles/github-flavored-markdown) syntax. (This doesn’t include the GitHub-specific features like Task Lists or @mentions.) That gives you _fenced code blocks_:

<pre><code class="language-markdown">```
function test() {
  console.log("Hello, world");
}
```</code></pre>

You may also specify the language:

<pre><code class="language-markdown">```javascript
function test() {
  console.log("Hello, world");
}
```</code></pre>

```javascript
function test() {
  console.log("Hello, world");
}
```

Harp will serve the code block as HTML:

```html
<pre><code class="language-javascript">function test() {
  console.log(&quot;Hello, world&quot;);
}</code></pre>
```

The `language-` class name follows the [W3C](http://www.w3.org/TR/html5/text-level-semantics.html#the-code-element) and [WHATWG](http://www.whatwg.org/specs/web-apps/current-work/multipage/text-level-semantics.html#the-code-element) convention for specifying the type of code, which means client-side highlighters like [Prism](http://prismjs.com/) work out of the box.

## Markdown is not a template engine

Markdown is rendered to static HTML by [`marked`](https://marked.js.org/). It doesn’t execute template code, so the following don’t work inside the body of a `.md` file:

- `<%= variable %>` and `<%- variable %>` interpolation
- `partial()` calls
- `<% if (...) %>` and `<% for (...) %>` blocks

The values from a `_data.json` entry or `_harp.json` globals **are** attached to the page’s render context — they’re just not visible inside the markdown body, because the markdown processor doesn’t reach for them.

In practice, this is fine: the surrounding `_layout.ejs` (which is a real EJS template) can read those variables and use them for the `<title>` tag, navigation, related-post lists, and any other chrome. The `.md` file itself stays pure prose. If you need template logic inside the body of a page, write it as `.ejs` instead.

## Managing file extensions

You may want to create a markup file other than `.html` using Markdown. Just prefix `.md` with the desired extension. For example, `feed.xml.md` is served as `feed.xml`.

This trick is also possible (and often more useful) with [EJS](ejs) and [Jade](jade).

## Also see

* [Official Markdown documentation](http://daringfireball.net/projects/markdown/)
* [GitHub Flavoured Markdown documentation](https://help.github.com/articles/github-flavored-markdown)
* [On Markdown and the `partial` function](partial#markdown)
