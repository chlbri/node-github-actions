# cache-store

A composite GitHub Action that sets up pnpm caching and installs dependencies.

## Description

This action:

- resolves the pnpm store path
- restores or saves the pnpm cache using `actions/cache`
- installs dependencies with `pnpm install --no-frozen-lockfile`

## Usage

```yml
name: Cache Store Example
uses: chlbri/node-github-actions/.github/actions/cache-store@main
```
