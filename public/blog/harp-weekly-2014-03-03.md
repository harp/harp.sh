# Harp Weekly – Three Static Patterns

This edition of Harp Weekly includes plenty of patterns you can use when building a static site with Harp.

## Nested Layouts

Raymond Camden of Adobe has become a staple of Harp Weekly, and I couldn’t be happier about it! Last week, he [recorded a screencast](https://harp.sh/blog/harp-weekly-2014-02-24), and this week he will show you how you can use [nested layouts with Harp](http://www.raymondcamden.com/index.cfm/2014/2/27/Nested-Layouts-in-HarpJS).

## Writing short-form with Harp

> being able to code natively in Sass and Jade rather than CSS and HTML is frickin’ awesome.

[Short Form Blog wrote](http://shortformblog.com/post/77741855168/you-guys-were-writing-about-possible-alternatives-to)—briefly, as you might expect—about some of the benefits of Harp, and deploying to the [Harp Platform](https://www.harp.io).

## A client-side redirects recipe	

Redirects are important if you’re moving an existing site over to Harp. We’re looking at the best way to build this into Harp—or how to build on [contributions from the community](https://github.com/sintaxi/harp/pull/263). In the meantime, there’s a new recipe on a workaround for adding [client-side redirects](https://harp.sh/recipes/client-side-redirect).

## Adding next and previous links to your posts

Raymond also wrote about [adding next and previous links](http://www.raymondcamden.com/index.cfm/2014/2/26/Creating-NextPrevious-Links-in-HarpJS) to your static blog. This information is already available through the `_data.json` you’re writing, and Raymond will show you how to put it to good use:

[![](https://f.cloud.github.com/assets/1581276/1875335/658c8422-78f0-11e3-8c29-14ca87e320c6.png)](http://www.raymondcamden.com/index.cfm/2014/2/26/Creating-NextPrevious-Links-in-HarpJS)

You can also try out the [Baseline](https://github.com/rosshj/baseline) or [Remedy Harp boilerplates](https://github.com/kennethormandy/hb-remedy), which have this feature built-in.

## npm update

It’s worth noting that there was a change made to npm this week  that may require some changes to your setup. If you’re receiving a `SELF_SIGNED_CERT_IN_CHAIN` error when you try and install something through npm, [this blog post should help](http://blog.npmjs.org/post/78085451721/npms-self-signed-certificate-is-no-more).

## Next Harp Weekly

The next edition of Harp Weekly will feature community projects—[let me know](mailto:kenneth@chloi.io) if you’ve built something with Harp and would like to see it featured! Follow [Harp on Twitter](https://twitter.com/harpwebserver) to get the latest updates on Harp.