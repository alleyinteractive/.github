# Alley Community Health Files

This repository contains the default [community health
files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
for the [`alleyinteractive`](https://github.com/alleyinteractive) organization.

## Usage

This repository acts as a catch-all for Github organization-wide community
files, such as [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md). These community
health files will be used unless a repository has their own version.

The repository also contains reusable Github workflows for use on any public
repository. These workflows are reused across the organization to perform
continuous integration tests with Github Actions.

## Reusable Workflows

The following workflows are available to use:

- [Built Branch](#built-branch)
- [Built Tag](#built-tag)
- [Dependabot Auto Merge](#dependabot-auto-merge)
- [Dependabot Auto Approve](#dependabot-auto-approve)
- [Node Tests](#node-tests)
- [PHP Composer Script](#php-composer-script)
- [PHP Code Quality](#php-code-quality)
- [PHP Coding Standards](#php-coding-standards)
- [PHP Tests](#php-tests)
- [Deploy to Remote Repository](#deploy-to-remote-repository)

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
    tags:
      - 'v*.*.*'
      - '!*-built'

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
  pull_request:

permissions:
  pull-requests: write
  contents: write

jobs:
  dependabot:
    uses: alleyinteractive/.github/.github/workflows/dependabot-auto-merge.yml@main
```

### Dependabot Auto Approve

Automatically approves Dependabot pull requests for auto-merging when the
default branch for a repository is protected.

#### Usage

```yml
name: dependabot-auto-approve
on:
  pull_request:

permissions:
  pull-requests: write
  contents: write

jobs:
  dependabot:
    uses: alleyinteractive/.github/.github/workflows/dependabot-auto-approve.yml@main
```

### Node Tests

Run automated Node tests against your repository. Assumes that your plugin will
have the following commands available to it:

```sh
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

##### `ci`

- Specify if `npm ci` should be used versus `npm install`.
- Accepts a boolean.
- Defaults to `false`.

##### `cache`

- Specify the cache to use or otherwise disable.
- Will not cache if a `package-lock.json` is not found.
- Accepts a boolean.
- Defaults to `true`.

##### `run-audit`

- Specify if `npm audit --audit-level=high --production` should be run.
- Accepts a boolean.
- Defaults to `false`.

##### `run-test`

- Specify if `npm run test` should be run.
- Accepts a boolean.
- Defaults to `true`.

##### `run-lint`

- Specify if `npm run lint` should be run.
- Accepts a boolean.
- Defaults to `true`.

##### `run-build`

- Specify if `npm run build` should be run.
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

##### `dependency-versions`

- Allows you to select whether the job should install the locked, highest, or
  lowest versions of Composer dependencies.
- Accepts a string: `locked`, `highest`, or `lowest`.
- Defaults to `locked`.

##### `working-directory`

- Specify the working directory to use.
- Accepts a string.
- Defaults to the root of the repository.

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

### PHP Composer Script

Run a set of Composer scripts against your project. Assumes that `composer run
<command>` will run your tests. Supports multiple commands.

#### Inputs

> Specify using `with` keyword.

##### `command`

- Specify the Composer command to use for testing.
- Accepts a string.
- Required.

##### `php`

- Specify the PHP version to use.
- Accepts a number.
- Defaults to `8.0`.

##### `working-directory`

- Specify the working directory to use.
- Accepts a string.
- Defaults to the root of the repository.

#### Usage

```yml
name: Composer Tests

on:
  push:
    branches:
      - main
  pull_request:
  schedule:
    - cron: '0 0 * * *'

jobs:
  code-quality:
    uses: alleyinteractive/.github/.github/workflows/php-composer-command.yml@main
    with:
      command: |
        lint
        phpunit
```

### PHP Code Quality

Run `phpstan` tests against your project. Assumes that `composer run phpstan` will
run your tests.

#### Inputs

> Specify using `with` keyword.

##### `command`

- Specify the Composer command to use for testing.
- Accepts a string.
- Defaults to `phpstan`.

##### `php`

- Specify the PHP version to use.
- Accepts a number.
- Defaults to `8.0`.

##### `dependency-versions`

- Allows you to select whether the job should install the locked, highest, or
  lowest versions of Composer dependencies.
- Accepts a string: `locked`, `highest`, or `lowest`.
- Defaults to `locked`.

##### `working-directory`

- Specify the working directory to use.
- Accepts a string.
- Defaults to the root of the repository.

#### Usage

```yml
name: Code Quality

on:
  push:
    branches:
      - main
  pull_request:
  schedule:
    - cron: '0 0 * * *'

jobs:
  code-quality:
    uses: alleyinteractive/.github/.github/workflows/php-code-quality.yml@main
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

##### `multisite`

- Flag if WordPress should be installed with multisite. Sets the `WP_MULTISITE` flag.
- Accepts a boolean.
- Defaults to `false`.

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
  php-tests:
    uses: alleyinteractive/.github/.github/workflows/php-tests.yml@main
```

You can also use the PHP tests inside a Github Action Matrix to test against
multiple PHP/WordPress versions:

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
  php-tests:
    strategy:
      matrix:
        php: [8.0]
        wordpress: ["latest"]
    uses: alleyinteractive/.github/.github/workflows/php-tests.yml@main
    with:
      php: ${{ matrix.php }}
      wordpress: ${{ matrix.wordpress }}
```

### Deploy to Remote Repository

Uses rsync and git to deploy files/folders from a local GitHub action repository to a remote repository.

_Notes_:

- We do not leverage external actions to manage the SSH agent as we want to keep the code as simple/single-sourced as possible.
- We must manually manage the SSH keys for the remote repository. This is typically done by adding the private key to the GitHub action secrets and then adding the public key to the remote repository (eg. as a write deploy key).

#### Inputs

> Specify using `with` keyword.

##### `os`

- Specify the operation system to use.
- Accepts a string.
- Defaults to `ubuntu-latest`.

##### `remote_repo`

- Specify the remote repository to deploy to.
- Accepts a string.
- Required.

##### `remote_branch`

- Specify the remote branch to deploy to.
- Accepts a string.
- Defaults to the same branch name in the remote repo as the current running action.

##### `base_directory`

- Specify the base directory to sync from.
- Accepts a string.
- Defaults to the root of the repository (`.`). **NOTE** You likely want a trailing slash if you're syncing a subdirectory. (eg. `wp-content/`)

##### `destination_directory`

- Specify the destination directory to sync to.
- Accepts a string.
- Defaults to the root of the remote repository (`.`).

##### `exclude_list`

- Specify a comma-separated list of files and directories to exclude from sync.
- Accepts a string. (e.g. `.git, .gitmodules`)
- Defaults to `.git, .gitmodules`.

#### Secrets

> Specify using `secrets` keyword.

##### `REMOTE_REPO_SSH_KEY`

- Specify the SSH key to use for the remote repository (requires write access).
- Required.

#### Usage

Example deploy to VIP:

```yml
name: Deploy to VIP repository

on:
  push:
    branches:
      - production
      - preprod
      - develop

jobs:
  sync-to-vip:
    uses: alleyinteractive/.github/.github/workflows/deploy-to-remote-repository.yml@main
    with:
      remote_repo: 'git@github.com:wpcomvip/alley.git'
      exclude_list: '.git, .gitmodules, .revision, .deployment-state, .node_modules, no-vip'
    secrets:
      REMOTE_REPO_SSH_KEY: ${{ secrets.REMOTE_REPO_SSH_KEY }}
```

Example Deploy to Pantheon multidev sites labeled `preprod` and `develop`:

```yml
name: Deploy to Pantheon repository

on:
  push:
    branches:
      - preprod
      - develop

jobs:
  sync-to-pantheon:
    uses: alleyinteractive/.github/.github/workflows/deploy-to-remote-repository.yml@main
    with:
      remote_repo: 'ssh://codeserver.dev.SOME-PANTHEON-SITE_ID@codeserver.dev.SOME-PANTHEON-SITE_ID.drush.in:2222/~/repository.git'
      destination_directory: 'wp-content/'
      exclude_list: '.git, pantheon-mu-plugin'
    secrets:
      REMOTE_REPO_SSH_KEY: ${{ secrets.REMOTE_REPO_SSH_KEY }}
```
