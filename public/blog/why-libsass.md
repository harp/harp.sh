# Why Harp uses libsass

Sass is probably the most popular CSS preprocessor---and you should stop using it. That is, you should stop using the Ruby version: 

We chose to use <a href="http://libsass.org">libsass</a>, the C++ implementation of Sass, for adding SCSS preprocessing to Harp. Many other projects have chosen to support it alongside the Ruby implementation of Sass…

## Speed

As Harp is a web server, speed is very important.

## Drawbacks

This speed boost comes with a caveat: libsass and the Ruby version of Sass do not have feature parity. There are some features in Sass 3.2 that are not yet supported by libsass (and therefore Harp). One omission to watch for is `@extends` and silent classes, but these should be available in libsass by the end of the year.

Libsass does not currently support Sass’ indented syntax, so Harp does not either. [We’re actively discussing other options](https://github.com/sintaxit/harp/71) for supporting the indented syntax. In the meantime, keep feel to keep using the SCSS syntax, or [give Stylus a try](https://harp.sh/docs/development/stylus). It has a concise, whitespace significant syntax based off of Sass’.
