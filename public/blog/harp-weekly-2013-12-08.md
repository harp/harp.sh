# Harp Weekly – Appetisers

On Thursday, we shared the beginnings of [the Harp recipes section](https://harp.sh/recipes/)—patterns and snippets that might be useful when creating sites and apps with Harp.

So far, there are a number of useful static blog recipes: easily create [excerpts](https://harp.sh/recipes/blog-post-excerpts) for your blog posts, or use a partial to [add Disqus comments](https://harp.sh/recipes/blog-post-comments) to your site. We’ve already receive requests on Twitter for what to cover next. Make sure to reply to [@HarpWebServer](https://twitter.com/harp) if you’re looking for something specific and we’ll do our best to add it to the list.

## Middleware Recipes

After [last week’s focus](https://harp.sh/blog/harp-weekly-2013-12-01) on using Harp as middleware in a larger application, we’ve seen some patterns that could be middleware recipes soon, too.

### Simple Auth

Nuno Job has put together an example of adding [simple authentication to a Harp app](https://gist.github.com/dscape/016d04a447e6acde96b1). If you need a fast way to keep something private, this is one way to approach the problem.

### Syntax Highlighting

If you’re writing documentation or technical blog posts, adding syntax highlighting is nice detail to be able to include. Ole Petter Bang looked at [adding syntax highlighting to an Express application using Harp](https://gist.github.com/gnab/7915894), by modifying some its the preprocessing settings.

If you aren’t running your Harp application as middleware, there’s still a number of reliable client-side options for syntax highlighting. For [harp.sh](https://harp.sh), we’re using [Prism.js](http://prismjs.com/) to help illuminate the [Harp documentation](https://harp.sh/docs).

## Grunt-Harp updated

Harp can make build steps unnecessary, and it can also work as one. If your setup uses Grunt, you can still use Harp’s implicit preprocessing with [this Grunt task for Harp](https://github.com/shovon/grunt-harp). It received a minor updated this week.

## Next Harp Weekly

If you’re making something with Harp, let us know on Twitter, [@HarpWebServer](https://twitter.com/harpwebserver). I’d be happy to include your project in next week’s post!

[Subscribe to <cite>Harp Weekly</cite>](http://harpjs.us7.list-manage1.com/subscribe?u=af92eba03471187c8aa0266e7&id=74381fea66)