# Sync VSCode Theme from Monorepo (KS-11)

## Context

The `delightful-vscode` distribution repo needs to be synced with `delightful-design-system/vscode-theme/` (monorepo source at `~/Desktop/Working/Github/delightful-design-system/vscode-theme/`). The distro should be a standalone copy — fully functional on its own.

## What changes

### Files to copy from monorepo

| File | Action |
|------|--------|
| `scripts/generate-themes.mjs` | Replace (picks up new dark ANSI palette, updated function signatures) |
| `screenshots/VSCode-Dark.png` | Copy (new directory) |
| `screenshots/VSCode-Light.png` | Copy (new directory) |
| `README.md` | Copy, then convert image paths to raw GitHub URLs |

### Files to delete from distro

| File | Reason |
|------|--------|
| `scripts/generate-icon.mjs` | Dead weight — icon.png already committed |
| `scripts/icon.html` | Dead weight — icon.png already committed |

### Files to edit in distro

| File | Changes |
|------|---------|
| `package.json` | Bump version `0.5.0` -> `0.6.0`, add `author` field, add 3 keywords. Keep distro-specific `repository.url` and `bugs.url` pointing to `delightful-vscode`. |

### Files to regenerate

| File | How |
|------|-----|
| `themes/delightful-dark-color-theme.json` | Run updated `generate-themes.mjs` (new dark ANSI palette) |
| `themes/delightful-light-color-theme.json` | Run updated `generate-themes.mjs` (should be identical, but regenerate for consistency) |

## What stays unchanged

- `icon.png` — already in sync
- `LICENSE` — already present
- `.gitignore` — distro has extra `.vscode-test/` entry, reasonable
- `.vscodeignore` — distro has extra `.DS_Store` and `.conductor/` entries, reasonable
- `scripts/package.json` and `scripts/package-lock.json` — identical across repos

## Key decisions

- **README**: Copy monorepo version as-is. Convert screenshot paths to raw GitHub URLs (`https://raw.githubusercontent.com/kylesnav/delightful-vscode/main/screenshots/...`) for Marketplace rendering.
- **package.json URLs**: Keep `repository.url` and `bugs.url` pointing to `delightful-vscode` (standalone repo).
- **CHANGELOG**: Skip for now.
- **Icon scripts**: Remove from distro.

## Verification

- Distribution repo files match monorepo source (except distro-specific overrides)
- README images use raw GitHub URLs
- Theme JSONs regenerated with updated dark ANSI palette
- No stale `.vsix` binaries in git
- `icon.png` renders correctly (unchanged)
