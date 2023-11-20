# Continuous Integration (CI) GitHub Actions for JS Single Page Application

This GitHub Action is optimized for testing and building JavaScript Single Page Applications, particularly projects set up with [Vite](https://vitejs.dev/). 

## Assumptions

- `yarn test`: A script for running tests. If your project doesn't have tests, ensure you add `"test": "echo \"no tests\""` to the `scripts` section of your `package.json`.
- `yarn build`: A script for building your project. This can be customized using the `build-command` parameter (see below).

## Basic Usage

```yaml
name: Test

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: nexys-system/gh-actions-spa-test@v1.1.7
```


## Parameters

This action supports a range of input parameters for customization:

- `build-command`: Specifies the build command to run. 
   - Default: `VITE_VERSION=${GITHUB_REF##*/} VITE_GIT_SHA=$GITHUB_SHA yarn build`

- `nodeversion`: Specifies the Node.js version to use.
   - Default: `20`

- `use-cache`: Determines whether to cache Yarn dependencies based on the `yarn.lock` file.
   - Default: `true`

- `deploy-project-name`: Specifies the project name for the deploy service. If this and `deploy-token` are provided, the action will attempt to deploy your application.

- `deploy-token`: Specifies the token needed for deployment. If this and `deploy-project-name` are provided, the action will attempt to deploy your application.

### Usage Example with Multiple Parameters

```yaml
...
- uses: nexys-system/gh-actions-spa-test@v1.1.6
  with:
    build-command: yarn buildprod
    nodeversion: '14'
    use-cache: 'false'
    deploy-project-name: 'my-spa-project'
    deploy-token: ${{ secrets.DEPLOY_TOKEN }}
```

In this example, the action is customized with a new build command, a different Node.js version, disabling cache, and providing deployment details.

## Deployment Configuration

For deploying your application through [Nova](https://nova.nexys.io), you need to set the following parameters:

- `deploy-project-name`: Specifies the project name for the deploy service.
- `deploy-token`: Specifies the token needed for deployment.

If the `deploy-project-name` and `deploy-token` are not provided, the deployment step is skipped, and a message is logged.

## Docker Integration

To generate a Docker container for your application, refer to the [gh-actions-docker-spa](https://github.com/nexys-system/gh-actions-docker-spa) repository for a compatible action.
