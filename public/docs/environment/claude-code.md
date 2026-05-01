# Claude Code skill

Authoring Harp projects with [Claude Code](https://docs.claude.com/en/docs/claude-code) becomes easier when Claude has explicit knowledge of Harp’s conventions. The [`harp-skills`](https://github.com/sintaxi/harp-skills) repository provides a Claude Code skill that supplies exactly that — layouts, partials, `_data.json`, the asset pipeline, the `_harp.json` schema, and the modern project shape.

When the skill is installed, Claude consults it automatically whenever it detects a Harp project (a `_layout.ejs`, `_data.json`, or `_harp.json` somewhere in the tree). You don’t need to mention "Harp" explicitly.

## Installation

Clone the repository and symlink the skill directory into Claude Code’s skill search path.

### Globally (all projects)

```bash
git clone https://github.com/sintaxi/harp-skills.git
mkdir -p ~/.claude/skills
ln -s "$(pwd)/harp-skills/harp" ~/.claude/skills/harp
```

### Per-project

```bash
cd <your-project>
git clone https://github.com/sintaxi/harp-skills.git /tmp/harp-skills
mkdir -p .claude/skills
ln -s /tmp/harp-skills/harp .claude/skills/harp
```

Adjust the clone destination to wherever you want the skill source to live. Confirm the skill is loaded by listing available skills inside Claude Code.

## What it covers

The skill teaches Claude about:

- Project structure: served root, the underscore convention, directory-as-routing.
- Layouts and partials, with `<%- yield %>` and `<%- partial(...) %>`.
- `_data.json` semantics and variable precedence (data passed to `partial()` > page entry > globals).
- The asset pipeline: `.ejs`/`.md`/`.jade` → `.html`, `.scss`/`.less`/`.styl`/`.sass` → `.css`, `.coffee`/`.cjs`/`.jsx` → `.js`.
- The decision rule for picking `.ejs` vs `.md` for new pages.
- The `_harp.json` schema: `globals`, `basicAuth`, `$ENV_VAR` substitution, runtime `environment` global.
- The CLI: `harp <source>` to serve, `harp <source> <build>` to compile.
- Patterns for refactoring duplicated chrome into layouts and partials.

For full setup details, troubleshooting, and updates, see the [harp-skills repository](https://github.com/sintaxi/harp-skills).
