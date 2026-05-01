# CLI

The `harp` command-line interface has two forms: one to serve a project locally, and one to compile it to a directory of static files.

## Serve a project

```bash
harp <source>
```

Pointing `harp` at a directory starts a local web server that serves that directory. The directory you point at *is* the served root — its name doesn't matter. `public/`, `src/`, `mysite/`, anything works.

```bash
harp ./mysite
# Serving at http://localhost:9000
```

You can also serve the current directory:

```bash
harp .
```

While the server is running, edit your templates and refresh your browser to see changes.

### Flags

| Flag | Default | Purpose |
|------|---------|---------|
| `-p, --port <port>` | `9000` | Port to listen on |
| `-h, --host <host>` | `0.0.0.0` | Host to bind to |
| `-s, --silent` | off | Suppress request logging |
| `-v, --version` | — | Print the installed version |
| `--help` | — | Print usage |

```bash
harp ./mysite --port 3000
harp ./mysite -p 8080 --silent
harp -v
```

## Compile to static assets

```bash
harp <source> <build>
```

Add a second argument to compile the project to a directory of static HTML, CSS, and JavaScript:

```bash
harp ./mysite ./www
```

The output directory is created if it doesn't exist. Templates are rendered to their final extensions:

- `.ejs`, `.md`, `.jade` → `.html`
- `.sass`, `.scss`, `.less`, `.styl` → `.css`
- `.coffee`, `.cjs`, `.jsx` → `.js`

All non-source files (images, fonts, plain `.html`, video, etc.) are copied through unchanged. Underscore-prefixed files — `_layout.*`, `_partials/*`, `_data.json`, `_harp.json` (or legacy `harp.json`) — are not emitted; they're build-time only.

The compiled output is deployable to any static host: Amazon S3, Netlify, GitHub Pages, Cloudflare Pages, or your own server.

## Production mode

Set `NODE_ENV=production` to enable additional caching and to flag the build as production:

```bash
NODE_ENV=production harp ./mysite
NODE_ENV=production harp ./mysite ./www
```

Inside any template, the `environment` variable resolves to `"production"` (or `"development"` otherwise), and `globals.environment` is set the same way. This is useful for switching analytics scripts, asset URLs, or feature flags between environments:

```ejs
<% if (environment === "production") { %>
  <script src="/analytics.js"></script>
<% } %>
```

See [Environment](/docs/development/environment) for more on the runtime environment variable.

## Notes

- Direct requests to source files are blocked. `/about.md` returns 404; only the rendered URL `/about` works.
- The dev server has no live reload — refresh your browser to see changes.
- Underscore-prefixed files and directories (`_layout.ejs`, `_partials/`, `_data.json`, `_harp.json`) are never served and are excluded from the compiled output.
- To embed Harp inside an existing Express application instead of running it as a CLI, see [Lib](/docs/environment/lib).
