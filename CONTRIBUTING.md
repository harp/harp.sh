# Contributing

Thanks for considering contributing to the [Harp website](https://harp.sh).

## Documentation

<!-- List of pages that need work -->

## Blog Posts

<!-- Just technically how to do it -->

## Markup

<!-- Jade, Bootstrap classes, etc. -->

## Styles

<!-- Note about identity guide, and that you can @-mention Kenneth -->

This version of [harp.sh](https://harp.sh) uses [Bootstrap](https://github.com/twbs/bootstrap). Bootstrap is in `_bootstrap` and is not modified.

To override the default behaviour of Bootstrap, make a copy of the component in `_override` and import it. Make the changes on top of Bootstrap, removing the lines that will not change from the original.

For example, the main banner on harp.sh uses a `.jumbotron` class from Bootstrap, which is located in `_bootstrap/jumbotron.less`. This is augmented with additional styles, like the additional `.jumbotron-knockout` class, in `_overrides/jumbotron.less`

For quick and less modular changes, work with in a `.section` in `application.less`, using non-Bootstrap classes.
