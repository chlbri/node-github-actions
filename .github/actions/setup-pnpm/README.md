# setup-pnpm

A composite GitHub Action that checks out the repository, sets up Node.js, and installs pnpm.

## Description

This action:

- checks out the repository using `actions/checkout`
- installs Node.js via `actions/setup-node`
- installs pnpm using `pnpm/action-setup`

## Usage

```yaml
uses: chlbri/node-github-actions/.github/actions/setup-pnpm@main
```
