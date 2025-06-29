# Harp Weekly – Harp v0.11.1 is authsome

Harp v0.11.1 was released this week, adding support for [HTTP Basic Authentication](https://harp.sh/docs/development/basicauth). This makes it easy to password protect an entire Harp app.

![An animation showing how basic authentication works with Harp and a Project Hub.](https://harp.sh/blog/images/harp-weekly-basic-auth-project-hub.gif)

## Password protecting a static Project Hub

Last Harp Weekly, Brad Frost’s Project Hub was featured, originally introduced in his article for <cite>24 ways</cite>. He says a Project Hub

> consolidates all the key design and development materials onto a single webpage … (either publicly available or password protected), so that everyone involved in the team has easy access to it.
> __Brad Frost, [Project Hubs: A Home Base for Design Projects](http://24ways.org/2013/project-hubs/)__

With basic authentication, Harp is even better for Project Hubs, as you can quickly add password protection to an entire site needed. Jorge Pedret’s [Project Hub boilerplate for Harp](https://github.com/jorgepedret/harp-project-hub) is ready to support this; just update the `_harp.json` file.

## Install Harp

More examples of how to add basic authentication are now available in [Harp’s documentation](https://harp.sh/docs/development/basicauth). You can get started by installing or updating Harp with:

```sh
sudo npm install -g harp
```

You may omit `sudo` if you’re using Windows.

## Interviewed by BetaKit

BetaKit, a Canadian publication about emerging technology, [interviewed Harp’s Brock Whitten and Rob Ellis](http://www.betakit.com/vancouvers-harp-io-makes-web-publishing-open-and-easy/). The co-creators of the [Harp Platform](http://harp.io) and PhoneGap discuss Harp, the influence of the Apache Cordova/PhoneGap model, and web publishing in general:

> The point isn’t that we’re building this product, the point is that the web is the&nbsp;product
> __Brock Whitten, [Vancouver’s Harp.io makes web publishing open and easy](http://www.betakit.com/vancouvers-harp-io-makes-web-publishing-open-and-easy/)__

If you’re interested in part of the story behind Harp, I think you’ll enjoy this article by John Gray.

## No more configuration

Rob Ellis also wrote about at Harp’s implicit preprocessing, and why you might want to move away from configuration-dependant setups. He says [if you’re writing configuration to manage your assets, you’re doing it wrong.](http://silentrob.me/articles/no-more-config)

## Deploying Harp to Octohost

[Octohost](https://github.com/octohost/octohost) is a [Heroku](https://harp.sh/docs/deployment/heroku)-esque platform based on Docker, with support for Node and Harp. There’s [a default application](https://github.com/octohost/harp) ready for you to clone on GitHub if you’d like to try out deploying there.

[![A screenshot of the default Octohost and Harp application.](https://harp.sh/blog/images/harp-weekly-octohost.png)](https://github.com/octohost/harp)

### Speeding up Docker deploys with Harp and Octohost

Darron Froese’s has written a post on [speeding up Docker deploys](http://blog.froese.org//2013/12/17/speeding-up-docker-deploys/) for deploying Harp applications on Octohost. Froese’s studio is

> building a platform to help deploy simple sites for our clients. The platform is called Handbill, under the scenes it’s using Harp and octohost.
> __Darron Froese, [Speeding up Docker deploys](http://blog.froese.org//2013/12/17/speeding-up-docker-deploys/)__

## Recipes: Next/Prev links, RSS feeds

[The RSS feed recipe](https://harp.sh/recipes/blog-rss-feed) was improved this week, adding more details and comments.

There was also a request for how to create next and previous links in a static blog using Harp. I’ve started with [an examples on GitHub](https://github.com/sintaxi/harp/issues/189), and [hb-remedy boilerplate](https://github.com/kennethormandy/hb-remedy) boilerplate has been updated to have them, too. A full recipe is forthcoming! 

[![](https://harp.sh/blog/images/harp-weekly-hb-remedy-next-prev.png)](https://github.com/kennethormandy/hb-remedy)

If you have any questions about getting started with Harp, or suggestions for recipes you’d like to see, the [join the #harp IRC channel](https://harp.sh/community/chat)—it’s now available directly on [harp.sh](https://harp.sh).

## Next Harp Weekly

Another version of Harp is already in underway. Follow [@HarpWebServer](https://twitter.com/harpwebserver) on Twitter to be notified first.