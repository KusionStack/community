# Contribute to the KusionStack project

* [Pull requests](#pull-requests)
* [GitHub basic setup](#github-basic-setup)
    * [Prerequisites](#prerequisites)
    * [Contributor roles](#contributor-roles)
    * [Golang coding style](#golang-coding-style)
    * [Rust coding style](#rust-coding-style)
* [GitHub best practices](#github-best-practices)
    * [Submit issues before PRs](#submit-issues-before-prs)
    * [Issue tracking](#issue-tracking)
    * [Closing issues](#closing-issues)
* [GitHub workflow](#github-workflow)
    * [Configure your environment](#configure-your-environment)
* [Patch format](#patch-format)
    * [General format](#general-format)
    * [Best practices for patches](#best-practices-for-patches)
    * [Examples](#examples)
* [Reviews](#reviews)
    * [Review Examples](#review-examples)
* [Continuous Integration](#continuous-integration)
* [Contact](#contact)
* [Project maintainers](#project-maintainers)

The KusionStack project is an open source project licensed under the
[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

It comprises a number of repositories under the [GitHub KusionStack organization](https://github.com/KusionStack). Unless
explicitly stated otherwise, all the KusionStack repositories follow the
process documented here.

## Pull requests

All the repositories accept contributions via [GitHub Pull requests (PR)](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests). Submit PRs by following the [GitHub workflow](#github-workflow).

## GitHub basic setup

To get started, complete the prerequisites below.

### Prerequisites

- Review [Contributor roles](#contributor-roles) that require special Git 
  configuration.

- [Set up Git](https://help.github.com/en/github/getting-started-with-github/set-up-git). 
  
  >**Note:** The email address you specify must match the email address you 
  >use to sign-off commits.

- [Fork and Clone](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) the relevant repository at the 
  [KusionStack Project](https://github.com/KusionStack).

   Example: Your local clone should show `your-github-username`, as follows.
   `https://github.com/${your-github-username}/community`.

### Contributor roles

Special Git configuration is required for these contributors:

* [Golang coding style](#golang-coding-style)
* [Rust coding style](#rust-coding-style)

For all other contributor roles, follow the standard configuration, shown in
Prerequisites. 

### Golang coding style

* Review [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments) to avoid common `Golang` errors.
* Use `gofmt` to fix any mechanical style issues.

### Rust coding style

* Use `rustfmt` to fix any mechanical style issues. Rustfmt uses a style which conforms to the
[Rust Style Guide](https://github.com/rust-dev-tools/fmt-rfcs/blob/master/guide/guide.md).
* Use `clippy` to catch common mistakes and improve your Rust code.

You can install the above tools as follows.

```sh
$ rustup component add rustfmt clippy
```

## GitHub best practices

### Submit issues before PRs

Raise a GitHub issue **before** starting work on a PR.

* Our process requires an issue to be associated with every PR (see [patch format](#patch-format))

* If you are a new contributor, create an issue and add a comment stating 
that you intend to work on the issue. This notifies our team of the work you 
plan to do.

### Issue tracking

To report a bug that is not already documented, please open a GitHub issue for the repository in question.

If it is unclear which repository to raise your query against, first try to
get in [contact](#contact) with us. If in doubt, raise the issue
[here](https://github.com/KusionStack/community/issues/new) and we will
help you to handle the query by routing it to the correct area for resolution.

### Closing issues

Our tooling requires adding a `Fixes` comment to at least one commit in the PR, which triggers GitHub to automatically close the issue once the PR is merged:

```
pod: Remove token from Cmd structure

The token and pid data will be hold by the new Process structure and
they are related to a container.

Fixes #123

Signed-off-by: Name <email>
```

The issue is automatically closed by GitHub when the
[commit message](https://help.github.com/articles/closing-issues-via-commit-messages/) is parsed.

## GitHub workflow

KusionStack employs certain augmentations to a 
[standard GitHub workflow](https://guides.github.com/introduction/flow/). 
In this section, we explain these augmentations in more detail. Follow these guidelines when contributing to KusionStack repositories, except where noted below.

* Complete the [GitHub basic setup](#github-basic-setup) above before continuing.

* Ensure each PR only covers one topic. If you mix up different items in
  your patches or PR, they will likely need to be reworked.

* Follow a [topic branch method](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-branches) for development.

* Follow carefully the [patch format](#patch-format) for PRs.

* Apply the appropriate GitHub labels to your PR. This
  is particularly relevant to maintain [Stable branch backports](#stable-branch-backports).

  >**Note:** External contributors should use keywords, explained in the
  >link above. Labels may not be visible to external contributors. 

* [Rebase](https://help.github.com/en/github/using-git/about-git-rebase)
  commits on your branch and `force push` after each cycle of feedback.

### Configure your environment

Most [KusionStack repositories](https://github.com/KusionStack)
contain code written in the [Go language (golang)](https://golang.org) and [Rust language](https://www.rust-lang.org/). Please install Go 1.17+ and Rust 1.60 stable.

#### Fork and clone

In this example, we configure a Git environment to contribute to this very 
`Community` repo. We create a sample branch, incorporate reviewer feedback, and rebase our commits.

1. Fork the [upstream repository](https://help.github.com/articles/cloning-a-repository):

1. [Clone your forked copy of the upstream repository](https://help.github.com/articles/cloning-a-repository):

1. While on your *forked copy*, select the green button `Clone or download`
   and copy the URL. 

1. Run the commands below and **paste the copied URL** (previous step),
   so your real GitHub user name replaces `your-github-username` below.
  
```sh
$ dir="$GOPATH/src/github.com/KusionStack" 
$ mkdir -p "$dir"
$ cd "$dir"
$ git clone https://github.com/{your-github-username}/community
$ cd community
```
   
>**Note:** Cloning a forked repository automatically gives a remote `origin`.

#### Configure the upstream remote

Next, add the remote `upstream`. Configuring this remote allows you to
synchronize your forked copy, `origin`, with the `upstream`. The 
`upstream` URL varies by repository. We use the `upstream` from the Community for this example. 

1. Change directory into `community`. 

1. Set the remote `upstream` as follows. 

    ```sh
    $ git remote add upstream https://github.com/KusionStack/community
    ```

1. Run `git remote -v`. Your remotes should appear similar to these:

    ```
    origin  https://github.com/your-github-username/community.git (fetch)  
    origin  https://github.com/your-github-username/community.git (push)  
    upstream  https://github.com/KusionStack/community (fetch)  
    upstream  https://github.com/KusionStack/community (push)  
    ```

For more details, see how to [set up a git remote](https://help.github.com/articles/configuring-a-remote-for-a-fork).

#### Create a topic branch

1. Create a new "topic branch" to do your work on:

    ```
    $ git checkout -b fix-contrib-bugs
    ```

    >**Warning:** *Never* make changes directly to the `master` branch 
    >--*always* create a new "topic branch" for PR work.

1. Make some editorial changes. In this example, we modify the file that
   you are reading.

    ```
    $ $EDITOR CONTRIBUTING.md
    ```

   >**Note:** If editing in Windows make sure that all documents end with LF
   > and not CRLF. The CI system will fail if carriage returns are in the
   > document. Many editors support the ability to change this. There is a
   > tool called dos2unix available on Git Bash for Windows and also available
   > on Linux systems that can convert files to LF endings. See the
   > [Configuring Git to handle line endings](https://docs.github.com/en/github/getting-started-with-github/getting-started-with-git/configuring-git-to-handle-line-endings)
   > guide for more details on how to configure `git` to automatically insert
   > the correct line endings.

1. Commit your changes to the current (`fix-contrib-bugs`) branch. Assure
   you use the correct [patch format](#patch-format):

    ```
    $ git commit -as
    ```

1. Push your local `fix-contrib-bugs` branch to your remote fork:

    ```
    $ git push -u origin fix-contrib-bugs
    ```

   >**Note:** The `-u` option tells `git` to "link" your local clone with
   > your remote fork so that it knows from now on that the local repository
   > and the remote fork refer to "the same" upstream repository. Strictly 
   >speaking, this option is only required the first time you call `git push`
   >for a new clone.

1. Create the PR:
  - Browse to https://github.com/KusionStack/community.
  - Click the "Compare & pull request" button that appears.
  - Click the "Create pull request" button.

  >**Note:** You do not need to change any of the defaults on this page.

#### Update your PR based on review comments

Suppose you received some reviewer feedback that asked you to make some
changes to your PR. You updated your local branch and committed those
review changes by creating three commits. There are now four commits in your
local branch: the original commit you created for the PR and three other
commits you created to apply the review changes to your branch. Your branch
now looks something like this:

```sh
$ git log master.. --oneline --decorate=no
4928d57 docs: Fix typos and fold long lines
829c6c8 apply review feedback changes
7c9b1b2 remove blank lines
60e2b2b doh - missed one
```

>**Note:** The `git log` command compares your current branch 
>(`fix-contrib-bugs`) with the `master` branch and lists all the commits,
>one per line.

#### Git rebase if multiple commits

Since all four commits are related to *the same change*, it makes sense to
combine all four commits into a *single commit* on your PR. You need to
[git rebase](https://help.github.com/github/using-git/about-git-rebase)
multiple commits on your branch. Follow these steps.

1. Update the `master` branch in your local copy of the upstream
   repository:

    ```
    $ cd $GOPATH/src/github.com/KusionStack/community
    $ git checkout master
    $ git pull --rebase upstream master
    ```

    The previous command downloads all the latest changes from the upstream
    repository and adds them to your *local copy*.

1. Now, switch back to your PR branch:

    ```
    $ git checkout fix-contrib-bugs
    ```

1. Rebase your changes against the `master` branch.

    ```sh
    $ git rebase -i master
    ```

    Example output:

    ```sh
    pick 2e335ac docs: Fix typos and fold long lines
    pick 6d6deb0 apply review feedback changes
    pick 23bc01d remove blank lines
    pick 3a4ba3f doh - missed one
    ```

1. In your editor, read the comments at the bottom of the screen. 
   Do not modify the first line, `pick 2e335ac docs: Fix typos ...`. Instead, revise `pick` to `squash` at the start of all following lines.

    Example output:

    ```sh
    pick 2e335ac docs: Fix typos and fold long lines
    squash 6d6deb0 apply review feedback changes
    squash 23bc01d remove blank lines
    squash 3a4ba3f doh - missed one
    ```

1. Save your changes and quit the editor. Git puts you *back* into your
   editor. You will see all the commit *messages*. 

1. At top is your first commit, which should be in the 
   [correct format](#patch-format). Keep your first commit and delete 
   all the following commits, as appropriate, based on 
   the review feedback.

1. Save the file and quit the editor. Once this operation completes, the four
   commits will have been converted into a single new commit. Check this by
   running the `git log` command again:

    ```sh
    $ git log master.. --oneline --decorate=no
    3ea3aef docs: Fix typo
    ```

1. Force push your updated local `fix-contrib-bugs` branch to `origin`
   remote:

    ```sh
    $ git push -f origin fix-contrib-bugs
    ```

>**Note:** Not only does this command upload your changes to your fork, it
>also includes the *latest upstream changes* to your fork since you ran
>`git pull --rebase upstream master` on the master branch and then merged
>those changes into your PR branch. This ensures your fork is now "up to
>date" with the upstream repository. The `-f` option is a "force push". Since
>you created a new commit using `git rebase`, you must "overwrite" the old
>copy of your branch in your fork on GitHub. 

Your PR is now updated on GitHub. To ensure team members are aware of this,
leave a message on the PR stating something like, "Review feedback applied".
This notification allows the team to once again review your PR more quickly.

## Patch format

### General format

Beside the `Signed-off-by` footer, we expect each patch to comply with the
following format:

```
subsystem: One line change summary

More detailed explanation of your changes (why and how)
that spans as many lines as required.

A "Fixes #issue-id" comment listing the GitHub issue this change resolves.
This comment is required for the main patch in a sequence. See the following examples.

Signed-off-by: Contributors Name <contributor@foo.com>
```

### Best practices for patches

We recommend that each patch fixes one thing. Smaller patches are easier to 
review, more likely to be accepted and merged, and more conducive for
identifying problems during review.

A PR can contain multiple patches. These patches should generally be related 
to the [main patch](#main-patch) and the overall goal of the PR. However, it 
is also acceptable to include additional or 
[supplementary patches](#supplementary-patch) for things such as:

- Formatting (or whitespace) fixes
- Comment improvements
- Tidy up work
- Refactoring to simplify the codebase

### Examples

#### Main patch

The following is an example of a full patch description for the main change that shows the required "`Fixes #issue-id`" comment, which references the GitHub issue this patch resolves:

```
pod: Remove token from Cmd structure

The token and pid data will be hold by the new Process structure and
they are related to a container.

Fixes: #123

Signed-off-by: Name <email>
```

#### Supplementary patch

If a PR contains multiple patches, [only one of those patches](#main-patch) needs to specify the "`Fixes #issue-id`" comment. Supplementary patches have an identical format to the main patch, but do not need to specify a "`Fixes #issue-id`"
comment.

Example:

```
image-builder: Fix incorrect error message

Fixed an error message which was referring to an incorrect rootfs
variable name.

Signed-off-by: Name <email>
```

## Reviews

Before your PRs are merged into the main code base, they are reviewed. We
encourage anybody to review any PR and leave feedback.

See the [PR review guide](PR-Review-Guide.md) for tips on performing a 
careful review.

We use the GitHub [Required Reviews](https://help.github.com/articles/approving-a-pull-request-with-required-reviews/)
system for reviewers to note if they agree or disagree with a PR. To have
an acknowledgment or "nack" registered with GitHub, you **must** use the
GitHub "Review changes" dialog to leave feedback. Notes left only in the
comments fields, whilst sometimes useful, will not get registered
in the acknowledgment counting system.

Documentation PRs can sometimes use a modified process explained in the
[Documentation Review Process](Documentation-Review-Process.md) guide.

### Review Examples

The following is an example of a valid "ack", as long as
the "Approve" box is ticked in the Review changes dialog:

```
Excellent work - thanks for your contribution.

lgtm
```

## Continuous Integration

The KusionStack project has a gating process to prevent introducing
regressions. When your PR is submitted, a Continuous Integration (CI) system
will run different checks on different platforms, based upon your changes.

All CI jobs must pass in order to merge your PR.

## Contact

The KusionStack community can be reached
[through various channels](README.md#join-us).

## Project maintainers

The KusionStack project maintainers are the people accepting or
rejecting any PR. Although [anyone can review PRs](#reviews), only the
acknowledgement (or "ack") from an Approver counts towards the approval of a PR.

Approvers are listed in GitHub teams, one for each repository. The project
uses the
[GitHub required status checks](https://help.github.com/en/articles/enabling-required-status-checks)
along with the [GitHub `CODEOWNERS`file](https://help.github.com/en/articles/about-code-owners) to specify who can approve PRs. All repositories are configured to require:

- Two approvals from the repository-specific approval team.

- One [documentation team](https://github.com/orgs/KusionStack/teams/documentation/members) approval if the PR modifies documentation.

