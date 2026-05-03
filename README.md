# github-actions

A collection of reusable GitHub Actions and workflow automation patterns for Node.js repositories.

This repository is designed to host custom composite actions and workflow templates that simplify common repository tasks such as installing dependencies, caching pnpm state, building packages, publishing releases, and tagging commits.

## Repository contents

- `.github/actions/setup-pnpm` — checkout repository, install Node.js, and install pnpm.
- `.github/actions/cache-store` — restore/save pnpm cache and install dependencies.
- `.github/actions/pnpmi` — combined `setup-pnpm` + `cache-store` for a reusable Node.js dependency install step.
- `.github/actions/tag` — create a GitHub git tag using `mathieudutour/github-tag-action`.
- `.github/workflows/ci.yml` — reusable CI workflow for testing the repository.
- `.github/workflows/publish.yml` — reusable publish workflow for npm packages and git tag creation.
- `.github/workflows/upgrade.yml` — admin maintenance workflow that runs maintenance scripts, bumps version, and commits changes.

## Custom actions

### `./.github/actions/setup-pnpm`

Sets up the repository, installs Node.js, and installs pnpm.

Usage:

```yaml
uses: chlbri/node-github-actions/.github/actions/setup-pnpm@main
```

### `./.github/actions/cache-store`

Restores or saves the pnpm cache, then installs dependencies with `pnpm install --no-frozen-lockfile`.

Usage:

```yaml
uses: chlbri/node-github-actions/.github/actions/cache-store@main
```

### `./.github/actions/pnpmi`

A reusable composite action that runs both `setup-pnpm` and `cache-store` to prepare the repository for Node.js work.

Inputs:

- `branch` (optional) — branch name to test

Usage:

```yaml
uses: chlbri/node-github-actions/.github/actions/pnpmi@main
with:
  branch: main
```

### `./.github/actions/tag`

Creates a GitHub tag using the provided tag name and GitHub token.

Inputs:

- `tag` (required)
- `token` (required)

Usage:

```yaml
uses: chlbri/node-github-actions/.github/actions/tag@main
with:
  tag: 1.2.3
  token: ${{ secrets.GITHUB_TOKEN }}
```

## Workflows

### `ci.yml`

A reusable CI workflow that:

- checks out the repository via `pnpmi`
- runs linting
- builds the package
- runs tests
- cleans up after test execution

### `publish.yml`

A reusable publish workflow that:

- builds the package
- publishes to npm using `JS-DevTools/npm-publish`
- creates a git tag when a publish occurs

### `upgrade.yml`

An administrative workflow that:

- runs repository maintenance scripts
- detects workspace changes
- bumps package version automatically
- commits the updated files back to the repository

## Getting started

Use this repository as a blueprint for reusable GitHub Actions in Node.js projects. Reference the local actions directly from workflows in this repository or import them into other repositories by using the GitHub path syntax.

Example workflow step:

```yaml
steps:
  - name: Install dependencies
    uses: chlbri/node-github-actions/.github/actions/pnpmi@main
    with:
      branch: main
```

## License

This repository is licensed under the terms of the included `LICENSE` file.
