# Continuous Integration (CI) GitHub Actions for JS Single Page Application

This GitHub Action is optimized for testing and building JavaScript Single Page Applications using [Bun](https://bun.sh/), particularly projects set up with [Vite](https://vitejs.dev/).

## Assumptions

- `bun test`: A script for running tests. If your project doesn't have tests, ensure you add `"test": "echo \"no tests\""` to the `scripts` section of your `package.json`.
- `bun run build`: A script for building your project. This can be customized using the `build-command` parameter (see below).

## Basic Usage

```yaml
name: Test

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: nexys-system/gh-actions-spa-test@v2.0.0
```

## Parameters

- `build-command`: Specifies the build command to run.
   - Default: `VITE_VERSION=${GITHUB_REF##*/} VITE_GIT_SHA=$GITHUB_SHA bun run build`

- `dist-path`: Path to the dist folder (relative to repo root).
   - Default: `dist`

- `deploy-project-name`: Specifies the project name for the deploy service. If this and `deploy-token` are provided, the action will attempt to deploy your application.

- `deploy-token`: Specifies the token needed for deployment. If this and `deploy-project-name` are provided, the action will attempt to deploy your application.

- `gzip-compression`: Compresses `.js`, `.css`, and `.html` files with gzip before deploying.
   - Default: `true`

### Usage Example (monorepo with deploy)

```yaml
name: Deploy

on:
  push:
    tags:
      - v*

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: nexys-system/gh-actions-spa-test@v2.0.0
        with:
          build-command: cd packages/client && VITE_GIT_SHA=$GITHUB_SHA VITE_VERSION=${GITHUB_REF##*/} bun run build
          dist-path: packages/client/dist
          deploy-project-name: my-project
          deploy-token: ${{ secrets.DEPLOY_TOKEN }}
```

## Deployment Configuration

For deploying your application through [Nova](https://nova.nexys.io), you need to set the following parameters:

- `deploy-project-name`: Specifies the project name for the deploy service.
- `deploy-token`: Specifies the token needed for deployment.

If the `deploy-project-name` and `deploy-token` are not provided, the deployment step is skipped.
