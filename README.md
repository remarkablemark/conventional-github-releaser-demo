# conventional-github-releaser-demo

This document goes over how to generate a GitHub release using [conventional-github-releaser](https://github.com/conventional-changelog/releaser-tools/tree/master/packages/conventional-github-releaser).

## Instructions

Commit a message that follows the [Conventional Commits](https://www.conventionalcommits.org/) format.

For [example](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines):

```sh
$ git commit -m 'feat: add new feature'
```

Run [`standard-version`](https://www.npmjs.com/package/standard-version):

```sh
$ npx standard-version
```

`standard-version` bumps the version and generates `CHANGELOG.md`.

Create a new [token](https://github.com/settings/tokens/new). Select the scope `public_repo` (or `repo` for access to private repositories).

Run [`conventional-github-releaser`](https://www.npmjs.com/package/conventional-github-releaser) with the token set as the environment variable:

```sh
$ CONVENTIONAL_GITHUB_RELEASER_TOKEN=<MY_TOKEN> npx conventional-github-releaser
```

`conventional-github-releaser` creates a GitHub release from the Git metadata.

Besides using the environment variable `CONVENTIONAL_GITHUB_RELEASER_TOKEN`, the token can also be passed via the flag `-t` or `--token`:

```sh
$ npx conventional-github-releaser -t <MY_TOKEN>
```

## FAQ

### Why is `conventional-github-releaser` failing with `GitHubError: Validation Failed (422)`?

This can happen for several reasons:

- The release for the version already exists on GitHub.
- The repository url is invalid in `package.json`.

See [conventional-changelog/releaser-tools#50](https://github.com/conventional-changelog/releaser-tools/issues/50) for more details.

### How can I debug `conventional-github-releaser`?

Set the environment variable `DEBUG=conventional-github-releaser` before running the command:

```sh
$ DEBUG=conventional-github-releaser npx conventional-github-releaser
```
