# Harp v0.18.0 – Node v4.0.0 compatibility

Last week, [Node v4.0.0](https://nodejs.org/en/blog/release/v4.0.0/) was released. We’re very happy to see where things have landed with the Node.js Foundation: the future continues to look very promising for Node, and we’re excited to be a small part of that through work on [Harp](https://github.com/sintaxi/harp).

The following day, we updated Harp to be compatible with this new version of Node. You can install or update Harp v0.18.0 right now through npm:

```sh
npm install -g harp
```

Depending on your platform, you may need to preface this command with `sudo`:

```sh
sudo npm install -g harp
```

You can also configure npm to run [without needing it](https://docs.npmjs.com/getting-started/fixing-npm-permissions). If you haven’t tried Harp before, learn how to [get started quickly](https://harp.sh/docs/quick-start).

## Changes in Harp v0.18.0

- Node-sass updated to v3.3.2, thanks [@djensen47](https://github.com/djensen47) and [@stephenway](https://github.com/stephenway)
- We no longer have any modules that are pulled from GitHub, meaning if you don’t have git installed or can’t pull from GitHub for some reason, installing Harp shouldn’t fail. [I](https://github.com/kennethormandy) worked on this to help [close #425](https://github.com/sintaxi/harp/issues/425), which [@MakiMark](https://github.com/MakiMark) and others helped report. Thanks everyone!
- EJS is updated to v2.3.1. This means EJS Filters will no longer work, which have been removed from EJS. This will impact you if you are using the [hb-casper boilerplate](https://github.com/kennethormandy/hb-casper) (it has since been updated).
- Harp’s intelligent indifference on trailing slashes now works as well on Windows as it does on OS X, which [@sintaxi](https://github.com/sintaxi) and [I](https://github.com/kennethormandy) worked on
- [@sintaxi](https://github.com/sintaxi) and [I](https://github.com/kennethormandy) also worked on improving our tests on Windows, so keep using Harp on Windows and keep letting us know how it’s working for you!
- If you’re using Harp as middleware for Express, you can now access the

## Jade

Jade was not updated in this version of Harp, but if you are using it, please be sure to review the breaking changes [in the last version of Harp](/blog/v0-17-0#jade). Namely, please change all instances of `!!!` to `doctype`.

We’ll likely be updating to the latest release of Jade in the next version, so this warning will no longer be present.

## Sass

Harp now uses Sass v3.3.2, the latest version at this time. This should alleviate any issues with Node-sass compatible frameworks like Foundation, and includes new features that move Node- and Libsass even closer to parity with Ruby Sass.

## EJS

We have also updated [EJS to v2.3.4](https://github.com/mde/ejs/releases/tag/v2.3.4).

The only significant breaking change for Harp, is the removal of built-in filters, like `truncate`. The only boilerplate that made use of this was [hb-casper](https://github.com/kennethormandy/hb-casper), which has been updated accordingly. If you have any troubles with this, feel free to mention us on Twitter.

***

<div class="panel"><strong>Work with the Harp core team</strong><p>Using Harp, working on a front-end application, or involved in a large Node.js project? We work together as [Chloi](http://chloi.io) and are available for work starting in October.</p><p>If you need a team experienced in getting high quality project in JavaScript into the hands of real customers quickly, [feel free to email me](mailto:kenneth@chloi.io?subject=JS%20consulting).</p></div>

***

Thanks for using Harp and [mention us on Twitter](https://twitter.com/harpwebserver) if you have any questions!
