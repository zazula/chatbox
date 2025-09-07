# Fork notes (zazula/chatbox)

- Upstream: https://github.com/chatboxai/chatbox
- Fork: https://github.com/zazula/chatbox
- Purpose: keep a clean fork of the stock app for builds and small tweaks.
- Differences from upstream: repo hygiene only (expanded .gitignore to exclude local/build artifacts). No app code changes.

## Build and run

- Requirements:
  - Node 22.x (or the version specified in .nvmrc/.node-version, if present)
  - npm (lockfile is committed; prefer `npm ci` for reproducible installs)
- Install:
  ```bash
  npm ci
  ```
- Develop/run (check package.json scripts):
  ```bash
  npm run dev
  npm start
  ```
- Package (adjust to scripts/tools in package.json):
  ```bash
  # Example if using electron-builder
  npx electron-builder --mac dmg
  # Or via a package script
  npm run dist
  ```

## Syncing this fork with upstream

One-off setup (only if the `upstream` remote isn’t present):
```bash
git remote add upstream https://github.com/chatboxai/chatbox.git
```

Fast-forward `main` from upstream, then update the fork:
```bash
git fetch upstream
git checkout main
git merge --ff-only upstream/main
git push origin main
```

Optional alias to simplify syncing:
```bash
git config --global alias.sync-upstream '!f() { \
  git fetch upstream && \
  git checkout main && \
  git merge --ff-only upstream/main && \
  git push origin main; \
}; f'
# Usage: git sync-upstream
```

## Branching workflow

- Keep `main` in this fork identical to `upstream/main`.
- Make changes on feature branches off `main`:
```bash
git checkout -b feature/<short-desc>
```
- Push to this fork and open PRs as needed (to this fork or upstream).

## Ignore rules (summary)

- Node/dev artifacts: `node_modules/`, `*.log`, `.eslintcache`, `.stylelintcache`, `.turbo/`, `*.tsbuildinfo`, `.history/`
- Env and OS/editor: `.env`, `.env.*`, `.env.*.local`, `.DS_Store`, `.idea/`, `.vscode/` (optional)
- Electron build outputs: `dist/`, `out/`, `build/`, `release/build/`, `release/app/dist/`
- iOS (if present): `ios/build/`, `ios/DerivedData/`, `ios/Pods/`, `ios/**/xcuserdata/`
- Do not ignore: `package-lock.json`, electron-builder config, entitlements, patches/config in `release/app`

## Credits and license

This is a fork of [chatboxai/chatbox](https://github.com/chatboxai/chatbox). Original license and credits apply.
