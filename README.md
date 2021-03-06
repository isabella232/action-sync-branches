# Github Action Sync Branches

An action to create a pull request between two branches.

## Example Usage

This action can be used to create a sync pull request when a branch gets a closed PR. This helps to keep downstream branches in sync.

Here's an example of a `.github/workflows/*.yml` file to trigger the action:

```yml
name: Sync master/develop branches

on:
  push:
    branches:
      - master

jobs:
  create_sync_pull_request:
    runs-on: ubuntu-latest
    steps:
      - uses: dequelabs/action-sync-branches@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          pr-title: 'chore: merge master into develop'
          pr-reviewers: scurker
          pr-labels: chore
```

## Configuration

> Note: If you need to assign team reviewers you will need to use a [personal access token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line), as the `GITHUB_TOKEN` generated via an action does not have [right permissions to assign teams](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/authenticating-with-the-github_token#permissions-for-the-github_token).

- **github-token** (required) - needed to interact with github api
- **debug** (default: `false`) - logs github api interactions to console
- **head** (default: `master`, required) - head branch to sync from
- **base** (default: `develop`, required) - target branch for the created pull request
- **pr-template** (default: `.github/pull_request_template.md`) - path to pull request template
- **pr-body** - body of pull request, will use `pr-template` as the default if this is not specified
- **pr-title** (default: `chore: merge master into develop`, required) - title for the created pull request
- **pr-labels** - labels to add to the created pull request
- **pr-reviewers** - reviewers to tag on the created pull request
- **pr-team-reviewers** - team reviewers to tag on the created pull request
- **pr-assignees** - assignees to tag on the created pull request

## License

UNLICENSED
