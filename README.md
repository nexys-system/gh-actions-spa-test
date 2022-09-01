# Github Actions for Singe Page Application

Tests and builds

## Usage

```
name: Test

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: nexys-system/gh-actions-spa-test@v1.0.2
```

## Params

* `build-command`: build command. Default is: `VITE_VERSION=${GITHUB_REF##*/} VITE_GIT_SHA=$GITHUB_SHA yarn build`
* `nodeversion`: node version used for the build, by default `18`

## Docker

see for docker https://github.com/nexys-system/gh-actions-docker-spa
