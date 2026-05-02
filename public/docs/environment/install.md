# Install Harp

Harp runs on [Node.js](https://nodejs.org/download/), which is available for macOS, Windows, Linux, and SmartOS — start by installing it from the [Node.js website](https://nodejs.org/download/) if you don’t have it already. You don’t need to know any JavaScript to use Harp, just enough of the command line to run a few `npm` commands.

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
