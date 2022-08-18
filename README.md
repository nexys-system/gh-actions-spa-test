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

## Docker

see for docker https://github.com/nexys-system/gh-actions-docker-spa
