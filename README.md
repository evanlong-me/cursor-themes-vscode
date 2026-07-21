# Cursor Themes (Official) for VS Code

The official [Cursor](https://cursor.com) editor themes, extracted verbatim from `Cursor.app` (v3.12.17) and packaged as a plain VS Code theme extension. Unlike community ports, every color — workbench, terminal, and all syntax `tokenColors` rules — is byte-identical to the real Cursor theme.

Themes included:

- **Cursor Dark**
- **Cursor Light**
- **Cursor Dark Midnight**
- **Cursor Dark High Contrast**
- **Cursor Light Colorblind (Beta)**

## Install

Download `cursor-themes-x.y.z.vsix` from the [latest release](../../releases/latest), then:

```sh
code --install-extension cursor-themes-x.y.z.vsix
```

Reload VS Code, then `Cmd+Shift+P` → `Preferences: Color Theme` → pick e.g. **Cursor Dark**.

To follow the system appearance (dark/light auto-switching, like Cursor does):

```jsonc
{
  "window.autoDetectColorScheme": true,
  "workbench.preferredDarkColorTheme": "Cursor Dark",
  "workbench.preferredLightColorTheme": "Cursor Light"
}
```

## Updating the theme files

The JSON files under `themes/` are copied unmodified from:

```
/Applications/Cursor.app/Contents/Resources/app/extensions/theme-cursor/themes/
```

To sync with a newer Cursor release, re-copy those files and bump `version` in `package.json`.

## Disclaimer

This extension is not affiliated with or endorsed by Cursor or Anysphere. All theme design and color assets are the work of the Cursor team (original author: Ryo Lu) and remain their property; this repository only repackages them for use in VS Code. If you are the rights holder and want this taken down, please open an issue.
