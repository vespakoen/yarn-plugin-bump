# yarn-plugin-bump

Non-interactive dependency upgrade tool for Yarn 2

```bash
yarn bump
```

## Options

```bash
Usage:

$ yarn bump [--exclude #0] ...

Examples:

Check what packages need to be upgrade
  $ yarn bump

Check update for the lodash package
  $ yarn bump lodash

Check update for packages match "^gatsby-*"
  $ yarn bump "^gatsby-*"

Check packages exclude react and react-dom
  $ yarn bump --exclude react --exclude react-dom
```

## Using the plugin through GitHub action

Bumping all dependencies and devDependencies and push it to bump-all branch every saturday.

```yml
on:
  schedule: "0 0 * * 6"

name: Bumping dependencies

jobs:
  bump:
    - name: Checkout
      uses: actions/checkout@v2
      with:
        ref: master

    - name: Bump up Yarn 2 dependencies
      uses: cometkim/yarn-plugin-bump@master
      with:
        pattern: ".*"
        branch: dependencies/all

    - name: Sync dependency update branch with Pull Request
      uses: vsoch/pull-request-action@1.0.5
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        PULL_REQUEST_FROM_BRANCH: master
```
