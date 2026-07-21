# Cursor Themes for VS Code

## Project overview

A VS Code theme extension that recreates the [Cursor](https://cursor.com) editor's five signature color themes. There is no executable code in this repository — the entire extension is declarative JSON. The theme files were extracted from Cursor.app (last synced from v3.12.17, see the initial commit `d6cd033`) and are kept in sync with new Cursor releases.

- Publisher: `evanlong` (marketplace item: `evanlong.cursor-themes`)
- Versioning: semver in `package.json`; releases are tag-driven (see Deployment).

## Repository layout

```
package.json          Extension manifest — the only configuration file
themes/               The 5 VS Code color theme JSON files (the whole product)
images/               Screenshots used in README / marketplace listing
icon.png              Marketplace icon
.github/workflows/publish.yml   Tag-driven publish pipeline
```

No source code, no dependencies, no `node_modules`, no build step.

## The themes

`package.json` → `contributes.themes` registers all five themes. When adding, renaming, or removing a theme, update both the file in `themes/` and this list (label, `uiTheme`, path).

| Label | File | `uiTheme` |
|---|---|---|
| Cursor Dark Midnight | `themes/cursor-dark-midnight-color-theme.json` | `vs-dark` |
| Cursor Dark High Contrast | `themes/cursor-dark-hc-color-theme.json` | `hc-black` |
| Cursor Dark | `themes/cursor-dark-color-theme.json` | `vs-dark` |
| Cursor Light | `themes/cursor-light-color-theme.json` | `vs` |
| Cursor Light Colorblind (Beta) | `themes/cursor-light-colorblind-color-theme.json` | `vs` |

Each theme file is standard VS Code theme JSON:

- `colors` — workbench/UI color keys (~180–290 entries)
- `tokenColors` — TextMate grammar scopes with `foreground`/`fontStyle` (~130–250 entries)
- `semanticTokenColors` + `semanticHighlighting` — present in Cursor Dark, Cursor Light, and Colorblind; absent in Midnight and High Contrast

## Build and test

There is no build, test suite, or linter. Validation is:

- JSON validity: each `themes/*.json` must parse (files are minified single-line, matching the extraction output — keep them that way).
- Packaging smoke test: `npx -y @vscode/vsce package -o cursor-themes.vsix` (this is what CI runs; `*.vsix` is gitignored).
- Manual check: `code --install-extension cursor-themes.vsix`, then `Preferences: Color Theme` and inspect editor, workbench, and terminal colors.

## Release / deployment process

Releases are cut by pushing a `v*` tag; `.github/workflows/publish.yml` handles the rest. Nothing auto-increments versions:

1. Update `version` in `package.json`.
2. Commit, then tag `v<version>` — the tag **must exactly match** `package.json`'s version or the workflow fails.
3. Push the tag. The workflow packages the VSIX, publishes to the VS Code Marketplace (`VSCE_PAT` secret), and creates a GitHub Release with the VSIX attached.

## Conventions

- Theme JSON stays minified single-line (faithful to the Cursor.app extraction); do not reformat.
- The themes are a faithful recreation of Cursor's colors — changes should come from re-syncing against a new Cursor.app release, not from ad-hoc color tweaks.
- Commit history shows the pattern: small, single-purpose commits, often ending with `bump <version>` when a release is included.
- Documentation and comments are in English.
- The extension targets `engines.vscode: "*"` — avoid using theme keys that require a recent VS Code version.
