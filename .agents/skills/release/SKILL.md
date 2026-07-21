---
name: release
description: Cut a release of this VS Code theme extension (bump version, commit, tag, push, verify publish to the VS Code Marketplace). Use when the user asks to release, publish, ship a new version, or bump the version of cursor-themes.
---

# Release cursor-themes

Releases are tag-driven: pushing a `v*` tag triggers `.github/workflows/publish.yml`, which packages the VSIX, publishes to the VS Code Marketplace (`VSCE_PAT`), and creates a GitHub Release. The tag must exactly match `package.json`'s `version` or the workflow fails.

## Steps

1. Determine the new version (ask the user if not given; semver, patch by default).
2. Update `"version"` in `package.json`.
3. If the release includes theme/content changes, make sure they are already committed. Commit the version bump separately with a message like `bump <version>` (or fold it into the change commit per repo history).
4. Create the tag `v<version>` pointing at that commit.
5. Push the branch and the tag together: `git push && git push origin v<version>`.
6. Watch the workflow: `gh run list --limit 3` until the Publish run for the tag completes with `success`.
7. Verify the marketplace actually serves the new version (do not trust the workflow alone):

```bash
curl -s -X POST 'https://marketplace.visualstudio.com/_apis/public/gallery/extensionquery' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json;api-version=7.1-preview.1' \
  -d '{"filters":[{"criteria":[{"filterType":7,"value":"evanlong.cursor-themes"}]}],"flags":914}' \
  | python3 -c "import json,sys; e=json.load(sys.stdin)['results'][0]['extensions'][0]; print(e['versions'][0]['version'])"
```

It must print the new version. If it still shows the old one right after a successful run, wait a few minutes and re-check before declaring done.

## Notes

- Theme JSON files stay minified single-line; never reformat them during a release.
- There is no build/test step; `npx -y @vscode/vsce package` is the only smoke test, and CI runs it.
