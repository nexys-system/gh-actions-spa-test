# Continuous Integration (CI) Github Actions for JS Single Page Application

Tests and builds a JS application. This has been optimized for [vite](https://vitejs.dev/). We assume 

* `yarn test`: tests package. If you do not have any tests, make sure you add `"test": "echo \"no tests\""` in the `scripts` section of your `package.json`
* `yarn build`: builds package (can be overwritten with params, see below)

## Usage

```
name: Test

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: nexys-system/gh-actions-spa-test@v1.1.0
```

## Params

* `build-command`: build command. Default is (optimized for [vite](https://vitejs.dev/)): `VITE_VERSION=${GITHUB_REF##*/} VITE_GIT_SHA=$GITHUB_SHA yarn build`
* `nodeversion`: node version used for the build, by default `20`
* `use-cache`: caches yarn dependencies based on the `yarn.lock` file


### Usage example with params

```
...
- uses: nexys-system/gh-actions-spa-test@v1.1.0
  with:
    build-command: yarn buildprod
```

## Docker

To generate a docker container, have a look at https://github.com/nexys-system/gh-actions-docker-spa

## Deploy

From deploy.nexys.io, set the following variables:

* `deploy-project-name`
* `deploy-token`
