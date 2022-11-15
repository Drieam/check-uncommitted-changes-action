# Check uncommitted changes action

A GitHub action for checking if repository has uncommitted changes.

## Outputs

### `changes`

Changes outputted by `git status --porcelain`.

### Example usage

```yaml
name: Check uncommitted changes
jobs:
  check-uncommitted-changes:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          ref: ${{ github.head_ref }}
      - name: Make uncommitted changes by creating empty file
        run: touch uncommitted.tmp
      - name: Check for uncommitted changes
        id: check-changes
        uses: drieam/check-uncommitted-changes-action@v2
      - name: Evaluate if there are changes
        if: steps.check-changes.outputs.outcome == failure()
        run: echo "There are uncommitted changes"
```

Check uncommitted changes and print them out

```yaml
name: Check uncommitted changes and print them out
jobs:
  check-uncommitted-changes:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          ref: ${{ github.head_ref }}
      - name: Make uncommitted changes by creating empty file
        run: touch uncommitted.tmp
      - name: Check for uncommitted changes
        id: check-changes
        uses: drieam/check-uncommitted-changes-action@v2
      - name: Print uncommitted changes
        if: steps.check-changes.outputs.changes != ''
        run: echo "There are uncommitted changes"
```

Note: You can change the `id` of the step but remember to change the referencing `id` on the subsequent step(s).

## Inspired by

https://github.com/marketplace/actions/has-changes
