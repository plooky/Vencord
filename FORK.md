# Fork Maintenance

This fork tracks `Vendicated/Vencord` while keeping fork-specific plugins and install assets available from this repository.

## Upstream Sync

`.github/workflows/sync-upstream.yml` runs once a day and can also be started manually from the Actions tab. It fetches `Vendicated/Vencord`, merges `upstream/main` into this fork's `main`, and pushes the result back to `origin/main`.

If upstream changes conflict with fork-specific work, the workflow fails before pushing. Resolve the conflict locally, push `main`, then rerun the workflow.

## Install Assets

`.github/workflows/fork-build.yml` builds the fork on every relevant `main` push and publishes the contents of `dist/` to a stable release tag named `fork-build`.

For the web userscript, install:

```text
https://github.com/plooky/Vencord/releases/download/fork-build/Vencord.user.js
```

For a local desktop install from this fork:

```sh
pnpm install --frozen-lockfile
pnpm build
pnpm inject
```

## Fork Plugins

Shared fork plugins can live in `src/userplugins/<pluginName>/index.tsx`; this fork intentionally tracks `src/userplugins` so those plugins can be committed and included in fork builds.

Use `src/plugins/<pluginName>` only when a plugin should behave like a normal bundled Vencord plugin and appear in generated plugin metadata. Prefer unique plugin folder names to reduce future merge conflicts with upstream.
