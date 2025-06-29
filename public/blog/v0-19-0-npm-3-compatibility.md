# Harp v0.19.0 – npm@3 compatibility

Congrats to our friends at npm: [npm@3 is out of beta!](http://blog.npmjs.org/post/129378362260/npm-weekly-29-npm-3-out-of-beta-nick-out-of-the) We have updated Harp for npm@3. We thought this was pretty important, because (as Forrest of npm pointed out) [npm is using Harp](https://github.com/sintaxi/harp/issues/462#issuecomment-141297442) for documentation!

If you’d like to update to the latest version of [npm](https://npmjs.org), you can optionally run: `npm install -g npm@latest`. Then, install or update Harp v0.19.0:

```sh
npm install -g harp
```

Depending on your platform, you may need to preface these commands with `sudo`:

```sh
sudo npm install -g npm@latest
sudo npm install -g harp
```

You can also configure npm to run [without needing `sudo`](https://docs.npmjs.com/getting-started/fixing-npm-permissions). If you haven’t tried Harp before, learn how to [get started quickly](https://harp.sh/docs/quick-start).

![](/blog/images/harp-weekly-example-illustration.png)

## Changes in Harp v0.19.0

- Sass is updated [to v3.3.3](https://github.com/sass/node-sass/releases/tag/v3.3.3), which improves Node-sass on Node v4.0.0
- [Connect is updated to v2.30.2](https://github.com/sintaxi/harp/commit/3f2298da2c115c7c6ca17ad2ebfc5415a26c26aa), which ensures Harp is more secure when running it [as Express middleware](https://harp.sh/docs/environment/lib)
- Updates [Minify to v0.3.3](https://github.com/harp/minify), which includes updated versions of UglifyJS2 and HTML Minify
- Updates [LRU Cache to v2.7.0](https://github.com/isaacs/node-lru-cache)
- Changes Autoprefixer to be a PostCSS plugin: when using Harp, everything still works the same, but this will allow us to update Autoprefixer in the next version and supresses some console warnings in the meantime

## Changes in Harp v0.18.0

Only a few days ago we also released [Harp v0.18.0](/blog/v0-18-0-node-v4-compatiblity), which added Node v4.0.0 support and updated many of the preprocessors in Harp. Make sure to take a look at [those updates, too](/blog/v0-18-0-node-v4-compatiblity).

***

<div class="panel"><strong>Work with the Harp core team</strong><p>Using Harp, working on a front-end application, or involved in a large Node.js project? We work together as [Chloi](http://chloi.io) and are available for work starting in October.</p><p>If you need a team experienced in getting high quality project in JavaScript into the hands of real customers quickly, [feel free to email me](mailto:kenneth@chloi.io?subject=JS%20consulting).</p></div>

***

Thanks for using Harp and [mention us on Twitter](https://twitter.com/harpwebserver) if you have any questions!
