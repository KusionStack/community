# Contributing to KusionStack Projects

This document explains the common procedures expected by contributors while submitting code to KusionStack projects.

## Code of Conduct

Please read the [Code of Conduct](CODE_OF_CONDUCT.md) before submit your contribution.

## General workflow

Once a github issue is accepted and assigned to you, please follow general workflow in order to submit your contribution:

1. Fork the target repository under your github username.
2. Create a branch in your forked repository for the changes you are about to make.
3. Commit your changes in the branch you created in step 2. 
4. Push your commits to your remote fork.
5. Create a Pull Request from your remote fork pointing to the HEAD branch (usually `main` branch) of the target repository.
6. Check the github build and ensure that all checks are green.

### Sign CLA

If it was your first pull request, you need to sign our [CLA(Contributor License Agreement)](https://github.com/KusionStack/.github/blob/main/CLA.md). The only thing you need to do is to post a pull request comment same as the below format:

`I have read the CLA Document and I hereby sign the CLA`

If your CLA signature failed, you may find the solutions below:

* The comment must be in the same format as above, with no extra spaces, line breaks, etc.
* The git committer must be the same one who created the KusionStack PR

*Note*: Some projects will provide specific configuration to ensure all commits are signed-off. Please check the project's documentation for more details.

## Tests

Make sure your changes are properly covered by automated tests. We aim to build an efficient test suite that is low cost to maintain and bring value to project. Prefer writing unit-tests over heavy end-to-end (e2e) tests. However, sometimes e2e tests are necessary. If you aren't sure, ask one of the maintainers about the requirements for your pull-request.