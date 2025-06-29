# Harp v0.20.0 – Node v5.x compatibility

Harp v0.20.0 supports Node v5.x, and simultaneously removes support for Node v0.10.x. To upgrade to the latest version of Node.js, visit the [official site](https://nodejs.org). Then, to ugprade or install the most recent release of Harp, run the following command from your terminal:

```sh
npm install -g harp
```

Depending on your platform, you may need to preface these commands with `sudo`:

```sh
sudo npm install -g harp
```

You can also configure npm to run [without needing `sudo`](https://docs.npmjs.com/getting-started/fixing-npm-permissions). If you haven’t tried Harp before, learn how to [get started quickly](https://harp.sh/docs/quick-start).

![](/blog/images/harp-weekly-example-illustration.png)

## Changes in Harp v0.20.0

- Sass is updated [to v3.4.2](https://github.com/sass/node-sass/releases/tag/v3.4.2), which improves Node-sass on Node v5.x
- Autoprefixer is updated to the [latest version](https://github.com/postcss/autoprefixer/releases/tag/6.1.0)
- [Lodash](https://lodash.com/docs) is available within templates


## Using Lodash within templates


Now that [Lodash](https://lodash.com/docs) is exposed within templates, certain template code can be simplified. For example, if you wanted to only show the posts from a blog that contained a specific tag (in this case, `photos`), you could use Lodash to ensure the tags array (defined with [flexible metadata](/docs/development/metadata)) `_.includes()` that specific tag:

  ```
  ol
  for post in public._data
    if _.includes(post.tags, 'photos')
      li= post.title
  ```

  The corresponding [`_data.json` file](/docs/development/metadata), in this case, might look like:

  ```json
  {
    "post-1": {
      "title": "Hello, world",
      "tags": ["blog"]
    },
    "post-2": {
      "title": "My trip to Mars",
      "tags": ["photos", "vacation", "blog"]
    },
    "post-3": {
      "title": "On the way back to Earth",
      "tags": ["photos", "blog"]
    }
  }
  ```

  …but in your template, only `post-2` and `post-3` would be included, as `post-1` doesn’t include the `photos` tag.

  All the helpers available as part of Lodash are now available within Harp templates, and are described fully on the [Lodash docs](https://lodash.com/docs).

***

<div class="panel"><strong>Work with the Harp core team</strong><p>Using Harp, working on a front-end application, or involved in a large Node.js project? We work together as [Chloi](http://chloi.io) and are currently available for work.</p><p>If you need a team experienced in getting high quality project in JavaScript into the hands of real customers quickly, [feel free to email me](mailto:kenneth@chloi.io?subject=JS%20consulting).</p></div>

***

Thanks for using Harp and [mention us on Twitter](https://twitter.com/harpwebserver) if you have any questions!
