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
  - [Names and Namespaces for Open-Source PHP Packages](#names-and-namespaces-for-open-source-php-packages)
  - [Branch Names](#branch-names)
  - [Coding Style](#coding-style)
    - [Alley Coding Standard](#alley-coding-standard)
    - [Tests](#tests)
    - [Backward Compatibility](#backward-compatibility)
    - [Documentation](#documentation)
    - [Compiled Assets](#compiled-assets)
  - [Release Process](#release-process)
    - [Releases to WordPress.org](#releases-to-wordpressorg)

## Code of Conduct

Please read our [Code of Conduct](./CODE_OF_CONDUCT.md) to keep our open-source
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

All repositories should have a
[CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
file included with a specified owner for the project. Preferably a team or 2+
individuals would be marked as "owners" who are responsible for the project.
These owners are responsible for the maintainership of the project and
controlling the scope of features within the said project. They shall have the
final say on whether or not a feature request is a good fit for the scope of a
project.

## Best Practices

The following are some best practices that we strive for in all of our projects.
A project may override these where it makes sense. The respective project should
have an updated `CONTRIBUTING.md` included with information about best practices
for the project.

### Names and Namespaces for Open-Source PHP Packages

#### Package names

Package names should be written in lowercase. Words should be separated with hyphens.

* Recommended: `alleyinteractive/traverse-reshape`, `alleyinteractive/simple-laravel-roles`
* Not recommended: `alleyinteractive/traverse_reshape`, `alleyinteractive/simpleLaravelRoles`

WordPress packages should be prefixed with `wp-`.

* Recommended: `alleyinteractive/wp-bulk-task`, `alleyinteractive/wp-caper`
* Not recommended: `alleyinteractive/bulk-task`, `alleyinteractive/alley-wp-caper`

#### PHP namespaces

General PHP packages should use the `Alley\` top-level namespace.

* Recommended: `Alley\traverse()`
* Not recommended: `Traverse\traverse()`

WordPress packages should use the `Alley\WP\` top-level namespace.

* Recommended: `new Alley\WP\Bulk_Task()`, `Alley\WP\Path_Dispatch::instance()`, `Alley\WP\find_one_post()`
* Not recommended: `new Alley\Bulk_Task()`, `WP_Path_Dispatch\Path_Dispatch::instance()`, `Alley\find_one_wp_post()`

Functions in the global namespace should be prefixed with `alley_`. Objects in
the global namespace should be prefixed with `Alley_`.

* Recommended: `alley_loop_template_part()`, `Alley_Singleton`
* Not recommended: `ai_loop_template_part()`, `AI_Singleton`

Packages may implement their own sub-namespaces.

* General PHP example: `new Alley\Validator\One_Of()`
* WordPress example: `new Alley\WP\Elasticsearch_Extensions\Controller()`

Packages should use the `Internals` sub-namespace for functions and objects
that are meant to be exempt from semantic versioning rules.

* General PHP example: `Alley\Internals\`
* WordPress example: `Alley\WP\Internals\`

### Branch Names

The default branch for open-source repositories is `develop` for projects that
can be downloaded/submoduled into a project. Always work from the `develop`
branch and open up pull requests against it.

The default branch name of `develop` only applies to 'package' repositories that
have the intended purpose of being distributed in a standalone
plugin/library/framework/etc.

Other projects may use `main` as a default branch under specific circumstances, including:

- Hosted packages: those where the repository represents a hosted website.
- Projects that would never be submodule'd/downloaded directly into a project.
  For example a NPM package or Javascript library.
- Standalone repositories that are always considered canonical/final such as
  [.github](https://github.com/alleyinteractive/.github) or
  [https://github.com/alleyinteractive/mantle-ci](mantle-ci).

In general, projects should always reference a tagged version of a project and
never track `develop`/`dev-develop` directly. The `develop` branch is considered
'nightly' and unstable at all times and is subject to change without notice.
Releases that follow the [release process](#release-process) should always be
backward compatible and well documented via a `CHANGELOG`.

### Coding Style

If the project maintainer has any additional requirements, you will find them
listed here.

#### Alley Coding Standard

Code must generally follow the [Alley Coding
Standard](https://github.com/alleyinteractive/alley-coding-standards) which is a
modified version of the [WordPress Coding
Standards](https://developer.wordpress.org/coding-standards/wordpress-coding-standards/).

One exception to this are unit tests which follow Alley Coding Standards but are
stored in PSR-4-compliant file paths. For example, a class file created with a
file path of `src/feature/class-example.php` would have a unit test located at
`tests/Feature/ExampleTest.php`. Alley Coding Standards will be evolving to
embrace PSR-4 in the future for more of the codebase, but for now, this exception
is in place only for unit tests.

#### Tests

Contributions to projects should have tests associated with them. Failure to
include tests could result in your contribution being declined.

#### Backward Compatibility

All contributions must be backward compatible unless a breaking change is being
made intentionally. Breaking changes must follow [semantic
versioning](https://semver.org/) and publish a new major release with a call out
to the breaking change in the project's CHANGELOG.

#### Documentation

Ensure that the `README.md`, `CHANGELOG`, and any other documentation are
up-to-date with any changes made.

#### Compiled Assets

Repositories should not contain compiled/built assets within their main
branches. This includes minified CSS or built Javascript files. Repositories
should use a GitHub action to produce a `*-built` branches and tags. These built
branches/tags can be used as submodules or downloaded directly for external use.

You can use a [Built
Branch](https://github.com/alleyinteractive/.github#built-branch) or [Built
Tag](https://github.com/alleyinteractive/.github#built-tag) action to
automatically compile your Composer/Node dependencies into `*-built` branches
and tags.

### Release Process

The following is a release process for all projects. All projects must follow
[semantic versioning](https://semver.org/).

1. Starting from the default branch of the repository, create a release branch
   for your changes (`release/X.X.X` for example).
2. Update the `CHANGELOG` with the release's changes. Bump the version
   referenced within the project's files, including in the `readme.txt`,
   the main plugin file, etc, to the new version.
3. Open a pull request for your new release branch.
4. Once the pull request is approved, merge the pull request and create a new
   [release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository) for the project. The release name and tag name should be
   the version name prefixed with a `v`. For example when releasing version
   `1.0.0` of a project, the tag name and GitHub release name should be
   `v1.0.0`.

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
