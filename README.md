<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/VSCode-Dark.png" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/VSCode-Light.png" />
    <img src="https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/VSCode-Light.png" width="600" alt="VS Code — Delightful" />
  </picture>
</p>

<h1 align="center">Delightful for VS Code</h1>

<p align="center">
  Neo-brutalist color theme with warm OKLCH colors — light and dark variants.
</p>

---

## Features

- **Light and dark themes** — warm cream backgrounds (light) and amber-tinted dark backgrounds (dark)
- **OKLCH-derived colors** — every color computed in the OKLCH perceptual color space for uniform visual weight
- **Neo-brutalist aesthetic** — bold accents, warm neutrals, intentional contrast
- **400+ scope mappings** — comprehensive syntax highlighting across languages

## Screenshots

### Light Theme

![Delightful Light](https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/VSCode-Light.png)

### Dark Theme

![Delightful Dark](https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/VSCode-Dark.png)

## Install

### VS Code Marketplace

1. Open VS Code
2. Go to **Extensions** (Ctrl+Shift+X / Cmd+Shift+X)
3. Search for **"Delightful"**
4. Click **Install**
5. Open **Settings** > **Color Theme** and select **Delightful Light** or **Delightful Dark**

### Manual Install

```bash
git clone https://github.com/kylesnav/delightful-vscode.git
cd delightful-vscode
npx @vscode/vsce package
code --install-extension delightful-theme-*.vsix
```

## Syntax Highlighting

Each syntax scope maps to a specific color family with semantic intent:

| Scope | Color | Why |
|-------|-------|-----|
| Keywords | Pink | Brand accent — the most distinctive color in the palette |
| Strings | Gold | Warm, readable, distinct from code structure |
| Functions | Cyan | Cool counterpoint to warm keywords |
| Comments | Muted neutral | De-emphasized, italic — present but not competing |
| Numbers | Green | Universally associated with values/data |
| Properties | Soft pink | Related to keywords but secondary |
| Types | Bright cyan | Structural, related to functions but bolder |
| Constants | Red | Signals immutability and importance |

## Color Philosophy

Delightful uses the **OKLCH** perceptual color space to build its palette. Unlike HSL or hex, OKLCH guarantees that colors at the same lightness value actually *look* equally bright — so the theme feels balanced across every syntax scope.

The palette is organized into **7 color families** — neutral, pink, red, gold, cyan, green, and purple — each with 5 lightness stops. Semantic tokens map these primitives to roles (background, text, accent, danger, warning, info, success), and the theme generator converts everything to hex for VS Code compatibility.

Both light and dark variants share the same hue angles and chroma relationships. The difference is in lightness mapping: light mode uses high-lightness neutrals with mid-lightness accents, while dark mode inverts this with low-lightness neutrals and higher-lightness accents for readability.

## Regenerating Themes

If you modify the OKLCH palette in the generator, regenerate the theme files:

```bash
cd scripts && npm install
node generate-themes.mjs
```

The generator reads OKLCH token values and converts them to hex using [culori](https://culorijs.org/).

## Part of Delightful

This theme is part of the [Delightful Design System](https://github.com/kylesnav/delightful-design-system) — a neo-brutalist design system with warm OKLCH colors, available for VS Code, Obsidian, Ghostty, iTerm2, Starship, and more.

## License

[MIT](LICENSE)
