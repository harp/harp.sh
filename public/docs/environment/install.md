# Install Harp

To install Harp, you must first have [Node.js](https://nodejs.org/download/), which can be installed on OS X, Windows, Linux, and SmartOS. [Download it from the Node.js website.](https://nodejs.org/download/)

<div class="videoWrapper"><iframe width="853" height="480" src="//www.youtube.com/embed/SEA0G9kpVJM?rel=0" frameborder="0" allowfullscreen></iframe></div>

First, install [Node.js](https://nodejs.org/download/). Harp uses Node.js, but you don’t need to know about Node.js or even JavaScript to use Harp. Once it’s finished installing, you can install Harp using the mighty npm: Node.js’ package manager. You’ll use the command prompt to do this.

## On OS X and Linux

Access the command prompt using the Terminal application. On OS X, it’s located in Applications → Utilities → Terminal. On Ubuntu, find it in Applications → Terminal. Then, run the following command:

```bash
sudo npm install -g harp
```

You may skip using `sudo` if you have the appropriate privileges.

## On Windows

If you are using Windows, Node.js will have come with the Node.js Command Prompt application. Now, to install Harp via npm, type in:

```bash
npm install -g harp
```

**That’s it!** Verify the install with:

```bash
harp -v
```

To start serving any folder of templates, point `harp` at that directory:

```bash
harp ./mysite
# Serving at http://localhost:9000
```

For the full set of commands, flags, and compile options, see the [CLI reference](/docs/environment/cli).

## Updating Harp

To update to the latest release, run the same install command again — npm replaces the existing global version in place:

```bash
npm install -g harp
```

You may need to preface this command with `sudo`, depending on your setup. Verify the new version with `harp -v`.

### Troubles upgrading? Try clearing your cache

If you’re having trouble upgrading — especially if you have recently upgraded npm, or are getting an error message like `Error: Cannot find module 'minify'` — clear the npm cache and reinstall:

```bash
npm uninstall -g harp
npm cache clean --force
npm install -g harp
```

You may need to use `sudo` before any of those, depending on your setup. The `npm cache clean` part can take a moment depending on how much is cached.

[Need to uninstall Harp?](/docs/environment/uninstall)
