# delightful-vscode

VS Code color theme extension for Delightful light and dark themes.

## Source of Truth

`scripts/generate-themes.mjs` contains the OKLCH token snapshot and generates `themes/*.json`.

## Validate

```sh
cd scripts && npm install
node generate-themes.mjs
cd ..
git diff -- themes/
npx @vscode/vsce package
```

The theme JSON diff must be empty unless the palette or scope mapping intentionally changed.

## Editing Rules

- Do not hand-edit generated `themes/*.json`.
- Keep Marketplace metadata in `package.json` complete: publisher, icon, gallery banner, repository, categories, keywords, and engines.
- Keep `.vscodeignore` tight so packaged VSIX files exclude source-only files and screenshots.

## Screenshots

Screenshots should show real VS Code windows in both light and dark themes, with syntax highlighting visible. Refresh when palette, scope mapping, or editor chrome changes.
