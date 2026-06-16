# Stylus

Stylus is an efficient, dynamic and expressive CSS pre-processor. It supports both an indented and a more familiar CSS style syntax.

## Why?

Harp has baked in the best-of-bread pre-compilers automatically. This means you don't need to think about which assets to download, minified CSS or un-baked stylus files. Everything just works.

## Usage

Harp's Asset Pipeline is super easy to use. All the pre-compiling happens implicitly so there is nothing to setup. Just name your file with a `.styl` extension instead of `.css` and the Harp web server will see it as if it is an `.css` file.

## Example

In our project we have a `style.styl` and a `variables.styl` file in our `public/css` directory, like so:

```
myapp.harp.io/
    +- public/
        |- index.ejs
        +- css/
            |- style.styl     
            +- _variables.styl 
```

You would simple setup your `index.ejs` as follows

```html
<html>
	<head>
		<link href="css/style.css" type="text/css" rel="stylesheet">
	</head>
	<body>
		...
	</body>
</html>	
```

And your `style.styl` could referene the variables like this:

```stylus
@import "_variables.styl"
body
	font 12px Helvetica, Arial, sans-serif
```

## Managing Imports

If you are familiar with Sass, you will accustomed to naming your partials with a leading underscore. This is permitted with Stylus, but not required. Because of this, you must explicitly reference the leading underscore when using `@import` to bring in a partial. For example, if you have a partial called `_example.styl`, you must use import it using `@import "_example". Simply saying `@import "example"` will not work in Stylus.

## Using Nib

[Nib](https://stylus.github.io/nib/) is a library of mixins and utilities for Stylus. The fastest way to add Nib to your Harp app is to clone the Nib Git repository:

```sh
git clone https://github.com/stylus/nib.git /path/to/myapp.harp.io/public/css/_nib
```

Now, in `style.styl` from the previous example, I can bring in Nib.

```stylus
@import "_variables.styl"
@import "_nib"

body
    font: 12px Helvetica, Arial, sans-serif
    background: linear-gradient(top, white, black)
```

## Also see
- [Official Site](http://stylus-lang.com/)
- [Nib Documentation](https://stylus.github.io/nib/)
