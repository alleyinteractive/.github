# Contributing <!-- omit in toc -->

Thank you for taking the time to contribute to our open-source projects!
Contributions are welcome and you will be fully credited.

Please take the time to read and understand the contribution guide before
creating an issue or pull request.

- [Code of Conduct](#code-of-conduct)
- [Contribution Guidelines](#contribution-guidelines)
  - [Reporting Issues/Bugs](#reporting-issuesbugs)
- [Maintainership](#maintainership)
- [Best Practices](#best-practices)
  - [Branch Names](#branch-names)
  - [Coding Style](#coding-style)
    - [WordPress Coding Standard](#wordpress-coding-standard)
    - [Tests](#tests)
    - [Backward Compatibility](#backward-compatibility)
    - [Documentation](#documentation)
    - [Compiled Assets](#compiled-assets)
  - [Release Process](#release-process)
    - [Releases to WordPress.org](#releases-to-wordpressorg)

## Code of Conduct

Please read our [Code of Conduct](./CODE_OF_CONDUCT.md) to keep our open source
community approachable and respectable.

## Contribution Guidelines

Contributions to projects can be in the form of bug reports or feature requests
via issues or pull requests. Pull requests are the preferred method of
contribution to a project.

### Reporting Issues/Bugs

Issues are the best way to file a bug report for a project. Before filing an
issue, please check for the following:

- Attempt to replicate your problem to ensure it can be repeated and isn't
  coincidental.
- Ensure that your feature request is within the scope of the project. For
  example, please don't suggest adding Drupal support to a WordPress plugin. If
  you are unsure, try making a discussion post in the project to ask the project
  maintainers.
- Search the repository for an existing issue/pull request to your issue/feature
  request. Check to make sure that your issue wasn't already reported/requested.

## Maintainership

All repositories should have a [CODEOWNERS](codeowners) file included with a
specified owner for the project. Preferably a team or 2+ individuals would be
marked as "owners" who are responsible for the project. These owners are
responsible for the maintainership of the project and controlling the scope of
features within the said project. They shall have the final say on whether or not a
feature request is a good fit for the scope of a project.

## Best Practices

The following are best practices that we strive for in all of our projects. A
project may override these where it makes sense. The respective project should
have an updated `CONTRIBUTING.md` included with information about best practices
for the project.

### Branch Names

The default branch for repositories is `trunk`. Always work from the `trunk`
branch and open up pull requests against it.

Projects should always reference a tagged version of a project and never track
`trunk`/`dev-trunk`. The `trunk` branch is considered 'nightly' or 'unstable' at
all times and is subject to change without notice. Releases that follow the
[release process](#release-process) should always be backward compatible and
well documented via a `CHANGELOG`.

### Coding Style

If the project maintainer has any additional requirements, you will find them
listed here.

#### WordPress Coding Standard

Code must generally follow the [WordPress Coding
Standard](wordpress-coding-standard). Our projects follow the standards via a
[PHPCS ruleset](phpcs-ruleset) with some modifications from core to allow for
some flexibility.

#### Tests

Contributions to projects should have tests associated with them. Failure to
include tests could result in your contribution being declined.

#### Backward Compatibility

All contributions must be backward compatible unless a breaking change is
being made intentionally. Breaking changes must follow [semantic
versioning](semvar) and publish a new major release with a call out to the
breaking change in the project's CHANGELOG.

#### Documentation

Ensure that the `README.md`, `CHANGELOG`, and any other documentation are
up-to-date with any changes made.

#### Compiled Assets

Repositories should not contain compiled/built assets within their main
branches. This includes minified CSS or built Javascript files. Repositories
should use a GitHub action to produce a `*-built` branches and tags. These built
branches/tags can be used as submodules or downloaded directly for external use.

You can use a [Built Branch](built-branch) or [Built Tag](built-tag) action to
automatically compile your Composer/Node dependencies into `*-built` branches
and tags.

### Release Process

The following is a release process for all projects. All projects must follow
[semantic versioning](semvar).

1. Starting from the default branch of the repository, create a release branch
   for your changes (`release/1.0.0` for example).
2. Update the `CHANGELOG` with the release's changes. Bump the version
   referenced in the project to the new version, including in the `readme.txt`,
   the main plugin file, etc.
3. Create a pull request for your new release version.
4. Once approved, merge the pull request and create a new [release](releases)
   for the project. The tag name and release name should be the version name
   prefixed with a `v`. For example when releasing version `1.0.0` of a
   project, the tag name and GitHub release name should be `v1.0.0`.

   The description of the release should be the release notes from the
   `CHANGELOG`.
5. If applicable, check to ensure that the `*-built` tag and branch of your
   project were properly compiled via GitHub actions (see [compiled assets](#compiled-assets)).
6. You're done, celebrate! 🎉

#### Releases to WordPress.org

After creating a new release, projects that are published to WordPress.org
should automatically push a new release to WordPress.org. Consider using a
[GitHub Action](https://github.com/10up/action-wordpress-plugin-deploy) to
automate that process.

[codeowners]: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners
[built-branch]: https://github.com/alleyinteractive/.github#built-branch
[built-tag]: https://github.com/alleyinteractive/.github#built-tag
[wordpress-coding-standard]: https://developer.wordpress.org/coding-standards/wordpress-coding-standards/
[phpcs-rulset]: https://github.com/alleyinteractive/alley-coding-standards
[semvar]: https://semver.org/
[releases]: https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository