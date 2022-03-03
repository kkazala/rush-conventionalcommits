# Rush and Conventional Commits

![SPFx](https://img.shields.io/badge/SPFx-1.13-green.svg)
![Rush](https://img.shields.io/badge/maintained%20with-rush-blueviolet)

## Summary

The monorepo is managed by rush, with individual versioning  policy.
The solution solutions consists of 2 SPFx projects, which are used only for testing rush commands. To this end, these are just Node.js projects.

There are two custom **rush commands**:

- **rush commitlint** lints commit messages
- **rush changefiles** generates rush change files based on the commit messages. The version increment is calculated based on the conventional commits specification

### rush commitlint

**commit-msg** git hook invokes **rush commitlint** to automatically lint messages. In case the message doesn't have correct format, commit is aborted.

### rush changefiles

**post-commit** git hook invokes  **rush changefiles** to parse commit message, calculate version increment and generate change files.
Increment is calcualted based on [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/):

- **fix**: a commit of the type `fix` patches a bug in your codebase (this correlates with `PATCH` in Semantic Versioning).
- **feat**: a commit of the type feat introduces a new feature to the codebase (this correlates with `MINOR` in Semantic Versioning).
- **BREAKING CHANGE**: a commit that has a footer `BREAKING CHANGE:`, or appends a `!` after the type/scope, introduces a breaking API change (correlating with `MAJOR` in Semantic Versioning). A BREAKING CHANGE can be part of commits of any type.
- types other than `fix:` and `feat:` are allowed, for example @commitlint/config-conventional recommends `build:`, `chore:`, `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, and others.

If the commit is not `fix:`, `feat:`, or a breaking change, change files are not generated.
If the commit message was used in the previous commit, change file generation is also skipped.
The change filesa are automatically commited with `git commit --amend`

## Applies to

- [SharePoint Framework](https://aka.ms/spfx)
- [Rush](https://rushjs.io/)

## Solution

Solution|Author(s)
--------|---------
rush-conventionalcommits | Kinga Kazala

## Version history

Version|Date|Comments
-------|----|--------
1.0|02 March 2022|Initial release

## Minimal Path to Awesome

- Clone this repository
- Ensure that you are at the solution folder
- in the command-line run:
  - **rush install**
- edit **spfx-libraries\spfx-utils\src\libraries\utils\UtilsLibrary.ts** file
- in the command-line run:
  - **git commit -am "feat: UtilsLibrary.getCurrentDate() function added"**
- A new change file is crated in **common\changes\spfx-utils** folder

## Documentation

[Rush and Conventional Commits Series](https://dev.to/kkazala/series/17133)  on dev.to
