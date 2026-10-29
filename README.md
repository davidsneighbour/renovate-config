# renovate-config

Shared Renovate configuration for @dnbhq projects.

## Installation

Add a `renovate.json5` file to your repository root:

```json5
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>davidsneighbour/renovate-config"
  ]
}
```

## Included behavior

This preset provides:

- `config:best-practices` base preset
- Semantic commit type set to `chore`
- Dependency Dashboard disabled
- Scheduled updates on Friday and Saturday from 00:00-04:59 and 21:00-23:59 in the Asia/Bangkok timezone
- Docker image digest pinning, keeping tags as the intended update stream
- GitHub Actions pinning to full commit SHAs while preserving Renovate's version comments
- Pinned npm `devDependencies`
- npm minimum release age from Renovate's security preset, currently three days
- Renovate configuration migration PRs
- Abandoned dependency detection
- Weekly lockfile maintenance during the configured update window, with manual review required
- No general third-party dependency automerge
- Grouped automerge only for `@davidsneighbour/*` and `@dnbhq/*` packages, after normal Renovate checks such as npm minimum release age

Security updates handled specially by Renovate should keep Renovate's normal security behavior; this preset does not add a custom delay override for them.

See [`default.json`](./default.json) for full details.

## Release process

Releases are managed with [`release-it`](https://github.com/release-it/release-it) and the shared [`@dnbhq/release-config`](https://github.com/dnbhq/release-config) defaults in `.release-it.ts`:

- `npm run release` → recommended version bump from conventional commits
- `npm run release:minor` → force a minor release
- `npm run release:major` → force a major release
- `npm run release:dry` → preview a release without changes
- `npm run release:config` → print the merged release-it configuration

The process updates the package version and `CHANGELOG.md`, creates a Git tag, and creates a GitHub release when `GITHUB_TOKEN_CONTENT_PRIVATE` is available. Releases run only from a clean `main` branch. npm publication is disabled.
