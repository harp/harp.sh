# The Rules

### Five simple rules you can count on when making templates for a Harp Application.

Rather than offering a complex feature set, Harp has simple rules on how it works. Harp is a katana, not a swiss army knife. By understanding the rules, one will know how to effectively use harp.

1. ## Convention over Configuration.

    Harp will function with as little as a `public/index.html` file and **doesn't require any configuration** to get going. To add more routes just add more files. All harp's features are based off conventions that you will discover by learning the rest of these rules.

    Harp is about offering a sane development framework which follows established best practices. Harp is not designed to be everything to everyone, but what it does, it does perfectly.

    ### Design Rationale

    By using convention over configuration, Harp is easier to learn, which makes you more productive.

    ### Anatomy of a typical Harp application

    ```
    myapp.harp.io/                <-- root of your application
      |- harp.json                <-- configuration, globals goes here.
      +- public/                  <-- your application assets belong in the public dir
         |- _layout.jade          <-- optional layout file
         |- index.jade            <-- must have an index.html or index.jade file
         |- _shared/              <-- arbitrary directory for shared partials
         |   +- nav.jade          <-- a partial for navigation
         +- articles/             <-- pages in here will have "/articles/" in URL
             |- _data.json        <-- articles metadata goes here
             +- hello-world.jade  <-- should have at least one .html,  .jade, .md or .ejs file.
    ```

2. ## The root directory is public.

    Harp is a web server, so it can serve any directory, whether it contains a large Harp app, or a single `index.html` file.

    ```
    myapp.harp.io/
        |- index.html           <-- will be served
    ```

    ### Framework style

    Optionally, a Harp application can also run in _Framework Style_. When a project contains a `harp.json` file and an explicit `public/` directory, the `public/` directory will be served instead of the root. In Framework Style, Public assets belong in the `public/` directory. Assets outside of the public directory will not be served.

    ```
    myapp.harp.io/
      |- harp.json                <-- required harp.json file
      |- README.md                <-- won't be served
      |- secrets.txt              <-- won't be served
      +- public/                  <-- explicit public directory
          +- index.html           <-- will be served
    ```

3. ## Ignore those which start with underscore.

    Any files or directories that begin with underscore will be ignored by the server. This is the recommended naming convention for layout and partial files. Harp will honour this rule for both files and directories.

    ### Design Rationale

    By having a simple convention, it is easy to specify and identify which assets will not be served to the end user.

    ### Example

    ```
    myapp.harp.io/
      +- public/
          |- index.html            <-- will be served
          |- _some-partial.jade    <-- won't be served
          +- _shared-partials/     <-- won't be served
              +- nav.jade
    ```

4. ## Dead simple asset pipeline.

    Harp serves jade, ejs, stylus, less and coffee script. Just add an extension of `.jade`, `.ejs`, `.styl`, `.less` or `.coffee` to your file and harp's asset pipeline will do the rest.

    Harp automatically pre-compiles, just add the file extension, and reference its counterpart.

    ```
    myfile.md            ->        myfile.html
    myfile.jade          ->        myfile.html
    myfile.ejs           ->        myfile.html
    myfile.less          ->        myfile.css
    myfile.styl          ->        myfile.css
    myfile.scss          ->        myfile.css
    myfile.sass          ->        myfile.css
    myfile.coffee        ->        myfile.js
    ```

    If you like, you may explicitly specify which `mime type` the file will be served with, by prefixing the extension with the desired extension.

    ```
    myfile.html.jade     ->        myfile.html
    myfile.xml.jade      ->        myfile.xml
    ```

    This is optional, however, as every extension already has a default `mime type`.  Both of the following will be served as `myfile.css` , for example:

    ```
    myfile.less          ->        myfile.css
    myfile.css.less      ->        myfile.css
    ```

5. ## Flexible metadata

    Your files named `_data.json` are special and make data available to templates.

    ```
    myapp.harp.io/
      +- public/
          |- index.jade
          +- articles/
              |- _data.json        <-- articles metadata goes here
              |- hello-world.jade  <-- hello world article
              +- hello-brazil.jade <-- hello brazil article
    ```

    Your `_data.json` file may contain something like this:

    ```json
    {
      "hello-world": {
        "title": "Hello World.",
        "date": "Feb 28, 2013"
      },
      "hello-brazil": {
        "title": "Hello Brazil.",
        "date": "March 4, 2013"
      }
    }
    ```

    This information will be available in all templates as:

    ```js
    public.articles._data
    ```

    Additionally, because `hello-world` matches the filename of `hello-world.jade`, these variables will be made available in the `hello-world.jade` template when being served. This object is also available in all the templates as `public.articles._data.hello-world`.

    In our templates we may iterate over the articles with the following in your Jade file&hellip;

    ```jade
    for article, slug in public.articles._data
      a(href="/articles/#{ slug }")
        h2= article.title
    ```
