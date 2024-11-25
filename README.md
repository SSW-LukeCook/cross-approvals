# cross-approvals

This repository is a proof of concept for handling cross-approvals using GitHub pull requests.

## F5 steps

### GitHub app
Create a GitHub app using the permissions found [here](https://github.com/peter-evans/create-pull-request/blob/main/docs/concepts-guidelines.md#authenticating-with-github-app-generated-tokens). This is needed so the GitHub action has the permissions needed to:
- Write to the repository contents (for creating the markdown file)
- Write pull requests (so it can raise a PR)
- Attach the "approvers" team to the PR (while the previous permissions can be achieved using the default GitHub Actions token approach, this particular functionality doesn't work. We need the GitHub app to achieve this)
