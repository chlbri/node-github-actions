# tag

A composite GitHub Action that creates a Git tag using `mathieudutour/github-tag-action`.

## Description

This action:

- creates a GitHub tag with the provided `tag`
- uses the supplied `token` for authentication

## Inputs

- `tag` (required): Tag string to create
- `token` (required): GitHub token with write permissions

## Usage

```yaml
uses: chlbri/node-github-actions/.github/actions/tag@main
with:
  tag: 1.2.3
  token: ${{ secrets.GITHUB_TOKEN }}
```
