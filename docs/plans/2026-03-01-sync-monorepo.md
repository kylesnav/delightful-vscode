# Sync VSCode Theme from Monorepo — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Sync the `delightful-vscode` distribution repo with the monorepo's `vscode-theme/` directory so the distro is a standalone, up-to-date copy.

**Architecture:** Direct file sync from monorepo source (`~/Desktop/Working/Github/delightful-design-system/vscode-theme/`) to distribution repo (`/Users/kylesnav/conductor/workspaces/delightful-vscode/amsterdam/`), with targeted edits for distro-specific overrides (URLs, image paths). Theme JSONs are regenerated from the updated generator.

**Tech Stack:** Node.js (culori), VS Code extension packaging

---

### Task 1: Delete dead icon generation scripts

**Files:**
- Delete: `scripts/generate-icon.mjs`
- Delete: `scripts/icon.html`

**Step 1: Delete the files**

```bash
rm scripts/generate-icon.mjs scripts/icon.html
```

**Step 2: Verify deletion**

```bash
ls scripts/
```

Expected: only `generate-themes.mjs`, `package.json`, `package-lock.json`

**Step 3: Commit**

```bash
git add scripts/generate-icon.mjs scripts/icon.html
git commit -m "chore: remove unused icon generation scripts"
```

---

### Task 2: Copy screenshots from monorepo

**Files:**
- Create: `screenshots/VSCode-Dark.png`
- Create: `screenshots/VSCode-Light.png`

**Step 1: Create screenshots directory and copy files**

```bash
mkdir -p screenshots
cp ~/Desktop/Working/Github/delightful-design-system/vscode-theme/screenshots/VSCode-Dark.png screenshots/
cp ~/Desktop/Working/Github/delightful-design-system/vscode-theme/screenshots/VSCode-Light.png screenshots/
```

**Step 2: Verify files exist**

```bash
ls -la screenshots/
```

Expected: two PNG files

**Step 3: Commit**

```bash
git add screenshots/
git commit -m "feat: add VS Code theme screenshots from monorepo"
```

---

### Task 3: Sync generate-themes.mjs from monorepo

**Files:**
- Replace: `scripts/generate-themes.mjs`

**Step 1: Copy the updated generator**

```bash
cp ~/Desktop/Working/Github/delightful-design-system/vscode-theme/scripts/generate-themes.mjs scripts/generate-themes.mjs
```

**Step 2: Verify the key changes are present**

Check that `ansiDark` palette exists and `buildColors` takes two arguments:

```bash
grep -n 'ansiDark' scripts/generate-themes.mjs | head -5
grep -n 'function buildColors' scripts/generate-themes.mjs
```

Expected: `ansiDark` object found, `buildColors(t, ansiPalette)` signature

**Step 3: Commit**

```bash
git add scripts/generate-themes.mjs
git commit -m "feat: sync theme generator from monorepo (dark ANSI palette)"
```

---

### Task 4: Regenerate theme JSON files

**Files:**
- Regenerate: `themes/delightful-light-color-theme.json`
- Regenerate: `themes/delightful-dark-color-theme.json`

**Step 1: Install dependencies and run generator**

```bash
cd scripts && npm install && node generate-themes.mjs && cd ..
```

Expected output:
```
Generated:
  themes/delightful-light-color-theme.json
  themes/delightful-dark-color-theme.json
```

**Step 2: Verify dark theme has updated ANSI colors**

The dark theme should now have different ANSI black/red/green/yellow values from light. Check the dark theme for the new `ansiDark` values:

```bash
grep '"terminal.ansiBlack"' themes/delightful-dark-color-theme.json
```

Expected: `#1e1a16` (from `ansiDark`), NOT `#16100c` (old shared palette)

**Step 3: Verify light theme is unchanged**

```bash
diff <(git show HEAD:themes/delightful-light-color-theme.json) themes/delightful-light-color-theme.json
```

Expected: no diff, or minimal formatting-only changes

**Step 4: Commit**

```bash
git add themes/
git commit -m "feat: regenerate themes with distinct dark ANSI palette"
```

---

### Task 5: Update package.json

**Files:**
- Modify: `package.json`

**Step 1: Apply the following edits to `package.json`**

Changes needed:
1. Bump `"version"` from `"0.5.0"` to `"0.6.0"`
2. Add `"author": { "name": "Kyle Snavely" }` after `"publisher"`
3. Add 3 keywords to the keywords array: `"light-theme"`, `"dark-theme"`, `"design-system"`

Keep these distro-specific values unchanged:
- `"repository.url": "https://github.com/kylesnav/delightful-vscode"`
- `"bugs.url": "https://github.com/kylesnav/delightful-vscode/issues"`

The final `package.json` should look like:

```json
{
  "name": "delightful-theme",
  "displayName": "Delightful",
  "description": "A warm, neo-brutalist color theme from the Delightful Design System",
  "version": "0.6.0",
  "publisher": "kylesnav",
  "author": {
    "name": "Kyle Snavely"
  },
  "license": "MIT",
  "icon": "icon.png",
  "galleryBanner": {
    "color": "#fdf8f3",
    "theme": "light"
  },
  "engines": {
    "vscode": "^1.80.0"
  },
  "categories": [
    "Themes"
  ],
  "keywords": [
    "theme",
    "color-theme",
    "warm",
    "neo-brutalist",
    "oklch",
    "delightful",
    "light-theme",
    "dark-theme",
    "design-system"
  ],
  "contributes": {
    "themes": [
      {
        "label": "Delightful Light",
        "uiTheme": "vs",
        "path": "./themes/delightful-light-color-theme.json"
      },
      {
        "label": "Delightful Dark",
        "uiTheme": "vs-dark",
        "path": "./themes/delightful-dark-color-theme.json"
      }
    ]
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/kylesnav/delightful-vscode"
  },
  "homepage": "https://github.com/kylesnav/delightful-design-system",
  "bugs": {
    "url": "https://github.com/kylesnav/delightful-vscode/issues"
  }
}
```

**Step 2: Validate JSON**

```bash
node -e "JSON.parse(require('fs').readFileSync('package.json', 'utf8')); console.log('valid')"
```

Expected: `valid`

**Step 3: Commit**

```bash
git add package.json
git commit -m "chore: bump version to 0.6.0, add author and keywords"
```

---

### Task 6: Sync README with raw GitHub URLs

**Files:**
- Replace: `README.md`

**Step 1: Copy monorepo README**

```bash
cp ~/Desktop/Working/Github/delightful-design-system/vscode-theme/README.md README.md
```

**Step 2: Convert image paths to raw GitHub URLs**

Replace relative screenshot paths with absolute raw GitHub URLs so they render on VS Code Marketplace and Open VSX. The following replacements are needed:

- `screenshots/VSCode-Dark.png` -> `https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/VSCode-Dark.png`
- `screenshots/VSCode-Light.png` -> `https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/VSCode-Light.png`

There are 3 occurrences total in the `<picture>` block (two `srcset` and one `src`).

**Step 3: Update monorepo-relative install paths**

The monorepo README says `cd vscode-theme` — update this to reflect standalone repo usage:

Replace:
```
cd vscode-theme
npx @vscode/vsce package
```

With:
```
npx @vscode/vsce package
```

Replace:
```
cd vscode-theme/scripts
```

With:
```
cd scripts
```

**Step 4: Verify no relative image paths remain**

```bash
grep -n 'screenshots/' README.md
```

Expected: all matches should be raw GitHub URLs, not relative paths

**Step 5: Commit**

```bash
git add README.md
git commit -m "feat: sync README from monorepo with raw GitHub URLs for Marketplace"
```

---

### Task 7: Final verification

**Step 1: Check no .vsix binaries in git**

```bash
git ls-files '*.vsix'
```

Expected: no output (clean)

**Step 2: Check file tree matches expectations**

```bash
find . -not -path './.git/*' -not -path './.context/*' -not -path './scripts/node_modules/*' -not -name '.DS_Store' | sort
```

Expected files:
```
.
./.gitignore
./.vscodeignore
./LICENSE
./README.md
./docs
./docs/plans
./docs/plans/2026-03-01-sync-monorepo-design.md
./docs/plans/2026-03-01-sync-monorepo.md
./icon.png
./package.json
./screenshots
./screenshots/VSCode-Dark.png
./screenshots/VSCode-Light.png
./scripts
./scripts/generate-themes.mjs
./scripts/package-lock.json
./scripts/package.json
./themes
./themes/delightful-dark-color-theme.json
./themes/delightful-light-color-theme.json
```

**Step 3: Verify dark theme ANSI palette diverges from light**

```bash
grep '"terminal.ansiBlack"' themes/delightful-light-color-theme.json themes/delightful-dark-color-theme.json
```

Expected: different hex values for light vs dark

**Step 4: Verify README images are absolute URLs**

```bash
grep 'raw.githubusercontent.com' README.md
```

Expected: 3 matches (two srcset, one src)
