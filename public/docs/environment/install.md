# Install Harp

To install Harp, you must first have [Node.js](https://nodejs.org/download/), which can be installed on OS X, Windows, Linux, and SmartOS. [Download it from the Node.js website.](https://nodejs.org/download/)

<div class="videoWrapper"><iframe width="853" height="480" src="//www.youtube.com/embed/SEA0G9kpVJM?rel=0" frameborder="0" allowfullscreen></iframe></div>

First, install [Node.js](https://nodejs.org/download/). Harp uses Node.js, but you don’t need to know about Node.js or even JavaScript to use Harp. Once it’s finished installing, you can install Harp using the mighty npm: Node.js’ package manager. You’ll use the command prompt to do this.

Access the command prompt using your terminal application:

* **macOS:** Applications → Utilities → Terminal
* **Linux:** Applications → Terminal (or your distro’s equivalent)
* **Windows:** the Node.js Command Prompt application that came with Node.js

Then run:

```bash
npm install -g harp
```

If you get a permission error (`EACCES`), the recommended fix is to install Node.js via a version manager like [nvm](https://github.com/nvm-sh/nvm), [fnm](https://github.com/Schniz/fnm), [asdf](https://asdf-vm.com/), or [Volta](https://volta.sh/) so global packages don’t require root. As a one-off workaround you can prefix the command with `sudo`, but mixing `sudo npm` with unprivileged `npm` calls can leave files owned by root and break later installs — fixing permissions properly is the safer path.

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

To update to the latest release, run the same install command — npm replaces the existing global version in place:

```bash
npm install -g harp
```

Verify the new version with `harp -v`.

### Troubles upgrading? Try clearing your cache

If you’re having trouble upgrading — especially if you have recently upgraded npm, or are getting an error like `Error: Cannot find module 'minify'` — clear the npm cache and reinstall:

```bash
npm uninstall -g harp
npm cache clean --force
npm install -g harp
```

The `npm cache clean` step can take a moment depending on how much is cached.

[Need to uninstall Harp?](/docs/environment/uninstall)
