# turbo --parallel doesn't actually set --continue

The [docs say](https://turbo.build/repo/docs/reference/run#--continue) that `Specifying the --parallel flag will automatically set --continue to true unless explicitly set to false`. While this may have been true at some point, this is not the case in current versions of turbo.

## Repro

- Check out this repo
- Run `npm install`
- Run `npx turbo run build --concurrency 2 --parallel`

### Expected behavior

All 5 packages should build (and fail), consistent with `--continue`

### Actual behavior

Only 2 packages build (and fail), consistent with `--continue=false`

### Other notes

Running `npx turbo run build --concurrency 2 --parallel --continue` runs build for all 5 packages

## Recommended Resolution

Either:
- Update the documentation to match the current behavior, e.g. `When specifying the --parallel flag, you probably should also set --continue so that all tasks run`, OR
- Change the behavior to match the documentation