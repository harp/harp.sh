# Public and Private Assets

In Harp, "public" refers to *the served root* — the directory whose contents are exposed to the web. The directory doesn't have to be named `public/`; it’s whatever directory you point `harp` at when you run the server.

A served root is required to have a functioning Harp application. Anything outside it isn't reachable, and anything inside it whose name starts with an underscore (`_layout.ejs`, `_partials/`, `_data.json`, `_harp.json`) is also held back from the public web.

## How the served root is chosen

Three scenarios cover every Harp project. The behavior comes from how Harp resolves the served root based on which config file (if any) is present.

### 1. No config file

The simplest case. Whatever directory you point `harp` at *is* the served root.

```
mysite/                        <-- served root
  |- index.html                <-- will be served
  `- about.md                  <-- will be served
```

Run with `harp ./mysite`. There’s no separate "public" directory — the directory you serve is the public.

### 2. `_harp.json` in the served directory

The same as scenario 1, but with config. Drop a `_harp.json` directly into the served directory when you want globals, HTTP Basic Auth, or [environment-variable substitution](globals).

```
mysite/                        <-- served root
  |- _harp.json                <-- won’t be served (underscore convention)
  |- _layout.ejs               <-- won’t be served
  |- index.ejs                 <-- will be served
  `- about.md                  <-- will be served
```

Run with `harp ./mysite`. The underscore prefix on `_harp.json` keeps the config file from being served itself, while still being read by Harp at startup.

### 3. Legacy app-style (`harp.json` + `public/`)

Older Harp projects place `harp.json` (no underscore) in a parent directory alongside a literal `public/` subdirectory. When Harp sees that pattern, it resolves the served root to `<project>/public/` rather than the project root.

```
project-root/
  |- harp.json                 <-- legacy config; won’t be served
  |- README.md                 <-- won’t be served (outside the served root)
  |- secrets.txt               <-- won’t be served
  `- public/                   <-- served root
      |- index.html            <-- will be served
      `- about.md              <-- will be served
```

Run with `harp ./project-root`. This shape still works for backward compatibility, but new projects should prefer scenario 1 or 2 — point `harp` directly at the source directory.

## What’s not served

Two rules cover everything Harp keeps off the public web:

* **Files outside the served root** — only relevant in scenario 3, where files alongside `harp.json` (but outside `public/`) are unreachable.
* **Files inside the served root whose name starts with `_`** — `_layout.ejs`, `_partials/`, `_data.json`, `_harp.json`, and any other underscore-prefixed file or directory. This is the rule that lets layouts, partials, and metadata live next to your pages without being addressable as URLs.

## The `public` template variable

Harp exposes the served-root data tree to templates under a variable named `public` — for example, `public.articles._data` returns the metadata in `articles/_data.json`.

This variable is **always present**, regardless of scenario, and is **unrelated** to whether you have a literal `public/` directory on disk. The name is a coincidence of history; it’s just the namespace Harp uses for the served-root data tree. See [Metadata](metadata) for examples of using it.
