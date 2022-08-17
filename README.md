# Alley Community Health Files

This repository contains the default [community health
files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
for the [`alleyinteractive`](https://github.com/alleyinteractive) organization.

## Usage

The repository contains reusable Github workflows for use on any public
repository.


## Workflows

The following workflows are available to use:

### Built Branch

Create a `*-built` version of a branch for use in submodules.

#### Inputs

> Specify using `with` keyword.

##### `php`

- Specify the PHP version to use.
- Accepts a number.
- Defaults to `8.0`.

##### `node`

- Specify the Node version to use.
- Will not build front-end assets if none are found.
- Accepts a number.
- Defaults to `16`.

#### Usage

```yml
name: Create a -built branch

on:
  push:
    branches:
      - main

jobs:
  built-branch:
    uses: alleyinteractive/.github/.github/workflows/built-branch.yml@main
```

### Built Tag

Create a `*-built` version of a tag for use in submodules.

#### Inputs

> Specify using `with` keyword.

##### `php`

- Specify the PHP version to use.
- Accepts a number.
- Defaults to `8.0`.

##### `node`

- Specify the Node version to use.
- Will not build front-end assets if none are found.
- Accepts a number.
- Defaults to `16`.

#### Usage

```yml
name: Create a -built tag

on:
  push:
    branches:
      - main

jobs:
  built-tag:
    uses: alleyinteractive/.github/.github/workflows/built-tag.yml@main
```

### Dependabot Auto Merge

Sets Dependabot pull requests to auto merge once they meet the requirements for merging (passes CI, approval, etc. as defined by the protected branch).

#### Usage

```yml
name: dependabot-auto-merge
on:
  pull_request_target:

permissions:
  pull-requests: write
  contents: write

jobs:
  dependabot:
    uses: alleyinteractive/.github/.github/workflows/dependabot-auto-merge.yml@workflows
```

### Node Tests

Run automated Node tests against your repository. Assumes that your plugin will
have the following commands available to it:

```
npm run lint
npm run test
npm run build
```

#### Inputs

> Specify using `with` keyword.

##### `node`

- Specify the Node version to use.
- Will not run if none are found.
- Accepts a number.
- Defaults to `16`.

##### `cache`

- Specify the cache to use or otherwise disable.
- Will not cache if a `package-lock.json` is not found.
- Accepts a boolean.
- Defaults to `true`.

#### Usage

```yml
name: Node Tests

on:
  pull_request:

jobs:
  node-tests:
    uses: alleyinteractive/.github/.github/workflows/node-tests.yml@main
```

### PHP Coding Standards

Run `phpcs` tests against your project. Assumes that `composer run phpcs` will
run your tests.

#### Inputs

> Specify using `with` keyword.

##### `php`

- Specify the PHP version to use.
- Accepts a number.
- Defaults to `8.0`.

##### `wordpress`

- Specify the WordPress version to use.
- Accepts a string.
- Defaults to `latest`.

#### Usage

```yml
name: Coding Standards

on:
  push:
    branches:
      - main
  pull_request:
  schedule:
    - cron: '0 0 * * *'

jobs:
  coding-standards:
    uses: alleyinteractive/.github/.github/workflows/php-coding-standards.yml@main
```

### PHP Tests

Run PHPUnit tests against your project. Installs and configures MySQL for
WordPress unit testing. Assumes that `composer run phpunit` will run your unit
tests.

#### Inputs

> Specify using `with` keyword.

##### `action`

- Specify the Composer action to use (install/update).
- Accepts a string.
- Defaults to `install`.

##### `command`

- Specify the Composer command to use for testing.
- Accepts a string.
- Defaults to `phpunit`.

##### `os`

- Specify the operation system to use.
- Accepts a string.
- Defaults to `ubuntu-latest`.

##### `php`

- Specify the PHP version to use.
- Accepts a number.
- Defaults to `8.0`.

##### `wordpress`

- Specify the WordPress version to use.
- Accepts a string.
- Defaults to `latest`.

#### `dependency-versions`

- Allows you to select whether the job should install the locked, highest, or lowest versions of Composer dependencies.
- Valid values are `locked`, `highest`, or `lowest`.
- Defaults to `locked`.

#### Usage

```yml
name: Testing Suite

on:
  push:
    branches:
      - main
  pull_request:
  schedule:
    - cron: '0 0 * * *'

jobs:
  coding-standards:
    uses: alleyinteractive/.github/.github/workflows/php-tests.yml@main
```