# Cursor Themes for VS Code

A faithful recreation of the [Cursor](https://cursor.com) editor's signature look, lovingly crafted for VS Code. Every shade — workbench chrome, terminal ANSI colors, and syntax highlighting — is matched pixel-for-pixel to the real thing, so your editor feels instantly familiar.

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

## Keeping the themes fresh

The themes are kept in sync with the latest Cursor releases. Each update is published to the VS Code Marketplace and as a GitHub release.

