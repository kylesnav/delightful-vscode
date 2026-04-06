# delightful-vscode

VS Code color theme extension — warm OKLCH colors, light and dark variants.

## Source of Truth

Token values come from [delightful-design-system](https://github.com/kylesnav/delightful-design-system). The generator has its own embedded OKLCH palette as JS objects — no monorepo imports.

## Build

```sh
cd scripts && npm install
node generate-themes.mjs
```

Reads OKLCH token values, converts to hex via [culori](https://culorijs.org/), outputs theme JSON. Never edit `themes/*.json` directly — regenerate from the script.

## Key Files

- `scripts/generate-themes.mjs` — Theme generator with embedded OKLCH palette
- `themes/delightful-light-color-theme.json`, `themes/delightful-dark-color-theme.json` — Generated output (400+ scope mappings)
- `package.json` — VS Code extension manifest + Marketplace metadata
- `.vscodeignore` — Controls what goes into the packaged `.vsix`

## Publishing

Not yet published. When ready: `npx @vscode/vsce package` then `npx @vscode/vsce publish`.

## Conventions

- All colors start as OKLCH, get converted to hex for VS Code compatibility.
- 7 color families: neutral, pink, red, gold, cyan, green, purple.
- Syntax mapping has semantic intent (pink = keywords/brand, cyan = functions, gold = strings).
