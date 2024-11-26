# cross-approvals

This repository is a proof of concept for handling cross-approvals using GitHub pull requests.

## F5 steps

### GitHub app
Create a GitHub app using the permissions found [here](https://github.com/peter-evans/create-pull-request/blob/main/docs/concepts-guidelines.md#authenticating-with-github-app-generated-tokens). This is needed so the GitHub action has the permissions needed to:
- Write to the repository contents (for creating the markdown file)
- Write pull requests (so it can raise a PR)
- Attach the "approvers" team to the PR (while the previous permissions can be achieved using the default GitHub Actions token approach, this particular functionality doesn't work. We need the GitHub app to achieve this)

#### Repo secrets
Make sure you add the `APP_ID` and `APP_PRIVATE_KEY` secrets to the repo, so the workflow can authenticate.


### Teams
You will need 2 teams added to the GitHub Org:
`@YourOrg/salary-sacrifice-approvers`
and
`@YourOrg/salary-sacrifice-owners`

These are currently hard-coded

#### Salary Sacrifice Approvers
This group gets attached to PRs via the workflow file defined in this repo. This should be your "first round" approvers.

#### Salary Sacrifice Owners
This group is defined as a **code owner** of `requests/**/salary-sacrifice-*`, so when the workflow raises a PR with a new file matching that pattern, the code owners automatically get added to the PR and the PR cannot be merged ("approved") until a code owner reviews it.


### Repo settings
- All code must be committed via pull requests
- Pull requests must have at least 2 successful reviews
- New commits to a branch require new reviews


### Edits/request changes
If a request needs to be knocked back, the reviewer can leave a comment and request changes like they would any other pull request.

The person making the salary sacrifice request should go back to their issue and edit the issue description directly, and this will kick off another commit on their open feature branch/PR.

> [!IMPORTANT]
> The UX for editing a GitHub issue isn't great. We lose the form controls that come with the issue template, so the user is forced to edit raw markdown.

