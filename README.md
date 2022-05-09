# action-find-or-create-linear-issue

This is a [Github Action](https://github.com/features/actions) that finds or creates a [Linear](https://linear.app/) Issue for your Pull Request. The Linear Issue identifier (e.g. `ENG-123`) is prefixed to the title of the PR.

This is helpful when you're:

- Ensuring each Pull Request has a Linear Issue.
  //comment

## Inputs

| Input             | Description                                                                        | Required |
| ----------------- | ---------------------------------------------------------------------------------- | -------- |
| `github-token`    | GitHub token required to modify the PR title.                                      | ✅       |
| `linear-api-key`  | Linear API key generated from https://linear.app/settings/api . (e.g. `lin_api_*)` | ✅       |
| `linear-team-key` | Team key (e.g. ENG) for the created Linear issue.                                  | ✅       |

## Outputs

| Output                     | Description                                                    |
| -------------------------- | -------------------------------------------------------------- |
| `linear-issue-id`          | The Linear issue's unique identifier. (UUID)                   |
| `linear-issue-identifier`  | The Linear issue's human readable identifier. (e.g. `ENG-123`) |
| `linear-issue-number`      | The Linear issue's number. (e.g. the `123` of `ENG-123`)       |
| `linear-issue-title`       | The Linear issue's title.                                      |
| `linear-issue-description` | The Linear issue's description.                                |
| `linear-issue-url`         | The Linear issue's URL. (e.g. `https://...`)                   |
| `linear-team-id`           | The Linear teams unique identifier. (UUID)                     |
| `linear-team-key`          | The Linear teams key/prefix (e.g. `ENG`)                       |
| `did-create`               | `true` if a Linear issue was created using this action.        |

## Example usage

### Create Linear Issue on Pull Request

```yaml
name: Find or Create Linear Issue in Pull Request

on:
  workflow_dispatch:
  pull_request:
    branches:
      - main
    types: ["opened", "edited", "reopened", "synchronize"]

jobs:
  create-linear-issue-on-pull-request:
    runs-on: ubuntu-latest
    steps:
      - name: Find or create a Linear Issue
        id: findIssue
        uses: ctriolo/action-find-or-create-linear-issue@v1
        with:
          github-token: ${{secrets.GITHUB-TOKEN}}
          linear-api-key: ${{secrets.LINEAR_API_KEY}}
          linear-team-key: "ENG"
```
