# perekine-service

This repository contains the service code. When changes are pushed to this repository, it automatically triggers a build process in the `perekine-builder` repository.

## Architecture

```
perekine-service (code changes)
    │
    └──> triggers via repository_dispatch
            │
            ▼
        perekine-builder (orchestrates build)
            │
            ├──> checks out perekine-service code
            └──> reads config from perekine-config
```

## Workflow

1. Code changes are pushed to this repository
2. GitHub Actions workflow `.github/workflows/trigger-build.yml` is activated
3. The workflow dispatches a build event to `perekine-builder`
4. `perekine-builder` receives the event and starts the build process
5. The builder checks out this repository's code and reads configuration from `perekine-config`

## Setup Requirements

For the repository dispatch to work, you need to:

1. Create a GitHub Personal Access Token (PAT) with `repo` scope
2. Add it as a secret named `BUILD_TRIGGER_TOKEN` in this repository's settings
3. The PAT should have access to the `perekine-builder` repository
