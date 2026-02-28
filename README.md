# Delightful

A warm, neo-brutalist color theme for [Visual Studio Code](https://code.visualstudio.com), based on the [Delightful Design System](https://github.com/kylesnav/delightful-design-system).

## Features

- **Warm color palette** — OKLCH-based neutrals with a subtle warm tint (hue 70), never cold gray
- **Neo-brutalist aesthetic** — Solid shadows, bold accents, and a warm visual language
- **Light & dark variants** — Carefully tuned for both, with warm dark backgrounds and vibrant syntax
- **Semantic highlighting** — Enhanced token colors for variables, types, parameters, and more
- **7 accent color families** — Pink (primary), red (danger), gold (warning), cyan (info), green (success), purple (creative), and warm neutrals
- **Complete terminal palette** — 16-color ANSI palette matching the design system
- **Bracket pair colorization** — Using design system accent colors
- **Full workbench theming** — Activity bar, sidebar, tabs, status bar, command palette, and every panel

## Installation

### From VS Code Marketplace

1. Open VS Code
2. Go to **Extensions** (`Ctrl+Shift+X` / `Cmd+Shift+X`)
3. Search for **"Delightful"**
4. Click **Install**
5. Open **Command Palette** (`Ctrl+Shift+P` / `Cmd+Shift+P`)
6. Type **"Color Theme"** and select **Preferences: Color Theme**
7. Choose **Delightful Light** or **Delightful Dark**

### From Open VSX (VS Codium, code-server, etc.)

1. Open the Extensions panel
2. Search for **"Delightful"**
3. Click **Install**

### Manual Install

```bash
# Download the .vsix from GitHub Releases
code --install-extension delightful-theme-0.5.0.vsix
```

## Syntax Highlighting

| Scope | Color | Token |
|-------|-------|-------|
| Keywords | Pink | `accent-primary` |
| Strings | Gold | `accent-gold` |
| Functions | Cyan | `accent-cyan` |
| Comments | Muted neutral | `text-muted`, italic |
| Numbers | Green | `accent-green` |
| Properties | Soft pink | `pink-300` |
| Types / Classes | Cyan (brighter) | `accent-cyan` |
| Constants | Red | `accent-danger` |
| Operators | Neutral | `text-secondary` |
| Tags (HTML/JSX) | Pink | `accent-primary` |
| Attributes | Gold | `accent-gold` |

## Color Palette

All colors are derived from the Delightful Design System's OKLCH tokens:

| Role | Light | Dark |
|------|-------|------|
| Background | Warm cream (`bg-surface`) | Amber-tinted dark (`bg-surface`) |
| Text | Deep warm brown (`text-primary`) | Light cream (`text-primary`) |
| Accent | Hot pink / fuchsia | Lighter pink |
| Danger | Warm red | Bright red |
| Warning | Gold | Gold |
| Info | Cyan | Bright cyan |
| Success | Green | Bright green |

## Supported Languages

Tested across: JavaScript, TypeScript, Python, Rust, Go, CSS, SCSS, HTML, JSX/TSX, JSON, Markdown, YAML, TOML, Shell/Bash, SQL, C/C++, Java, Ruby, PHP, Swift, Kotlin.

## Design System

This theme is part of the [Delightful Design System](https://github.com/kylesnav/delightful-design-system) — a comprehensive token system built on OKLCH color science with a neo-brutalist visual language.

### Token Architecture

| Layer | Purpose |
|-------|---------|
| **Primitives** | Raw OKLCH values — neutrals (0–950) and seven accent families |
| **Semantic tokens** | Background, text, border, and accent colors for light/dark modes |
| **Syntax tokens** | Dedicated dark-mode syntax palette for optimal readability |

## Development

Theme files are generated from OKLCH tokens:

```bash
cd scripts
npm install
node generate-themes.mjs
```

The generator reads OKLCH token values and converts them to hex using [culori](https://culorijs.org/).

## License

[MIT](LICENSE)
