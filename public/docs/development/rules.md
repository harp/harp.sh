# The Rules

### Five simple rules you can count on when making templates for a Harp Application.

Rather than offering a complex feature set, Harp has simple rules on how it works. Harp is a katana, not a swiss army knife. By understanding the rules, you'll know how to use Harp effectively.

1. ## Convention over Configuration.

    Harp will function with as little as a single `index.html` (or `index.ejs`, or `index.md`) file and **doesn't require any configuration** to get going. To add more routes, just add more files. All of Harp's features are based on conventions you'll discover by learning the rest of these rules.

    Harp is about offering a sane development framework that follows established best practices. Harp is not designed to be everything to everyone, but what it does, it does perfectly.

    ### Design Rationale

    By using convention over configuration, Harp is easier to learn, which makes you more productive.

    ### Anatomy of a typical Harp application

    ```
    mysite/                     <-- the directory you point harp at
      |- _harp.json             <-- optional config; globals, basic auth, env-var substitution
      |- _layout.ejs            <-- optional layout, wraps your pages
      |- index.ejs              <-- must have an index file (.html, .ejs, .md, or .jade)
      |- about.md               <-- prose pages can be Markdown
      |- _partials/             <-- arbitrary directory for shared partials
      |   `- _nav.ejs           <-- partial for navigation
      `- articles/              <-- nested directory; pages here have "/articles/" in URL
          |- _data.json         <-- per-directory metadata
          `- hello-world.md     <-- a content page
    ```

    Run with `harp ./mysite` to serve locally, or `harp ./mysite ./www` to compile to a directory of static files. See the [CLI reference](/docs/environment/cli) for more.

2. ## The directory you serve is the root.

    Harp is a web server. Whatever directory you point it at becomes the served root — its name doesn't matter (`public/`, `src/`, `mysite/`, anything works). The simplest possible Harp application is a single `index.html` in any folder:

    ```
    mysite/
      `- index.html             <-- will be served at /
    ```

    Drop a `_harp.json` into that same directory when you want site-wide globals, HTTP Basic Auth, or `$ENV_VAR` substitution. Because the filename starts with `_`, the config file isn't itself served (see Rule 3).

    ### Framework Style (legacy)

    Older Harp applications use a parent directory containing a `harp.json` file alongside a `public/` subdirectory. When `harp.json` is present at the top level, Harp serves the `public/` subdirectory rather than the project root, and assets outside `public/` aren't served.

    ```
    project-root/
      |- harp.json              <-- legacy config file
      |- README.md              <-- won't be served (outside public/)
      |- secrets.txt            <-- won't be served
      `- public/                <-- served root
          `- index.html
    ```

    Both styles still work. New projects should prefer the simpler form above: a single source directory, with an optional `_harp.json` directly inside it.

3. ## Ignore those which start with underscore.

    Any files or directories that begin with an underscore are ignored by the server and excluded from the compiled output. This is how Harp marks layouts, partials, metadata, and configuration as internal.

    ### Design Rationale

    By having a simple convention, it's easy to specify and identify which assets will not be served to the end user.

    ### Example

    ```
    mysite/
      |- _harp.json             <-- won't be served (config)
      |- _layout.ejs            <-- won't be served (layout)
      |- index.ejs              <-- will be served at /
      |- about.md               <-- will be served at /about
      `- _partials/             <-- won't be served (entire directory)
          `- _nav.ejs
    ```

4. ## Dead simple asset pipeline.

    Harp compiles preprocessor source files to standard web output on the fly. Just add the source extension to your filename — no configuration, no build step.

    ```
    myfile.ejs           ->        myfile.html
    myfile.md            ->        myfile.html
    myfile.jade          ->        myfile.html

    myfile.scss          ->        myfile.css
    myfile.sass          ->        myfile.css
    myfile.less          ->        myfile.css
    myfile.styl          ->        myfile.css

    myfile.coffee        ->        myfile.js
    myfile.cjs           ->        myfile.js
    myfile.jsx           ->        myfile.js
    ```

    `.cjs` and `.jsx` go through esbuild, so modern JavaScript and JSX work without any configuration.

    If you like, you may explicitly specify the output extension by prefixing the source extension with the desired one:

    ```
    myfile.jade          ->        myfile.html
    myfile.xml.ejs       ->        myfile.xml
    ```

    This is optional; every source extension has a default output type. Both of the following serve at `myfile.css`:

    ```
    myfile.less          ->        myfile.css
    myfile.css.less      ->        myfile.css
    ```

5. ## Flexible metadata.

    Files named `_data.json` are special and make data available to templates in the same directory.

    ```
    mysite/
      |- index.ejs
      `- articles/
          |- _data.json         <-- articles metadata
          |- hello-world.md     <-- hello world article
          `- hello-brazil.md    <-- hello brazil article
    ```

    Your `_data.json` file may contain something like this:

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

    Because the `hello-world` key matches the filename `hello-world.md`, those variables are attached to that page’s render context. They’re reachable from the wrapping `_layout.ejs` and from any other template via `public.articles._data`. (For `.ejs` and `.jade` pages, the values are also usable directly inside the page body as `<%= title %>`; markdown bodies don’t interpolate variables — see [Metadata](metadata) for details.)

    The whole metadata object is also available globally as `public.articles._data`. That's how an index page enumerates the entries — for example, in EJS:

    ```ejs
    <% for (var slug in public.articles._data) { %>
      <% var article = public.articles._data[slug] %>
      <a href="/articles/<%= slug %>">
        <h2><%= article.title %></h2>
      </a>
    <% } %>
    ```
