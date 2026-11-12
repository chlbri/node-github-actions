# pnpmi-vp

Composite action that sets up pnpm, Void Zero (`vp`) and restores the Vite task cache.

## Description

This action:

- sets up pnpm and installs dependencies using the local `pnpmi` action
- sets up Void Zero via `voidzero-dev/setup-vp`
- restores `node_modules/.vite/task-cache` and exposes the cache key so the caller
  can save it with `actions/cache/save`

## Outputs

- `vite-task-cache-path`: directory of the Vite task cache (pass it to `actions/cache/save`)
- `vite-task-cache-key`: primary key of the restored Vite task cache (pass it to `actions/cache/save`)
- `vite-task-cache-hit`: `'true'` when the cache was restored by an exact key match
- `vite-task-cache-matched-key`: key that actually matched, empty on a miss

## Usage

```yaml
steps:
  - name: Checkout pnpm repo and voidzero
    id: pnpmi-vp
    uses: chlbri/node-github-actions/.github/actions/pnpmi-vp@main

  - run: vp install
  - run: vp run test

  - name: Save Vite Task cache
    if: success() && steps.pnpmi-vp.outputs.vite-task-cache-hit != 'true'
    uses: actions/cache/save@v6
    with:
      path: ${{ steps.pnpmi-vp.outputs.vite-task-cache-path }}
      key: ${{ steps.pnpmi-vp.outputs.vite-task-cache-key }}
```
