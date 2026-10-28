# ci-workflows

Shared, reusable GitHub Actions workflows for all MusDev99 repositories. Fix CI once here; every repo picks it up.

| Workflow | Use for | Checks |
|----------|---------|--------|
| `node-ci.yml` | Next.js, Astro, any npm project | `npm ci`, then `npm run verify` if defined, otherwise lint, `tsc --noEmit` and build; `npm test` if defined; `npm audit --omit=dev` |
| `python-ci.yml` | FastAPI / Flask projects | install, ruff (fatal errors only), compileall, pytest if tests exist, `pip-audit` |

## Use it

Add `.github/workflows/ci.yml` to a repo:

```yaml
name: CI
on:
  pull_request:
  push:
    branches: [main, master]
permissions:
  contents: read
jobs:
  ci:
    uses: MusDev99/ci-workflows/.github/workflows/node-ci.yml@main
    # with:
    #   audit-level: critical   # default: high
```

## Requirements

- This repo must be **public**, or (if private) set *Settings, Actions, General, Access* to allow your other repos to use it.
- Pin to `@main` for automatic updates, or to a tag (`@v1`) for stability.
