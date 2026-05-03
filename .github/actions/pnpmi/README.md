# pnpmi

A composite GitHub Action that sets up pnpm and installs dependencies for a repository.

## Description

This action:

- sets up Node.js and pnpm using the local `setup-pnpm` action
- caches and installs dependencies using the local `cache-store` action

## Inputs

- `branch` (optional): Branch to test.

## Usage

```yaml
name: Checkout pnpm repo
uses: chlbri/node-github-actions/.github/actions/pnpmi@main
with:
  branch: main
```
