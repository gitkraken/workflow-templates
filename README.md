# Workflow Templates

This repo is meant to be a collection of documentation and code snippets you can adapt to improve your dev workflows and efficiency. Some of the content will be generically applicable to your repos, regardless of where they live. But, some of it is very GitHub specific. We would be happy to add more specific content for other Git hosting providers. Feel free to make Issues and PRs to improve this repo.

**Table of Contents**

- [Branch Naming](#branch-naming)
- [Git Hooks](#git-hooks)
- [Commit Messages](#commit-messages)
- [Pull Requests](#pull-requests)

## Branch Naming

There are plenty of ways you might want to structure your branch naming. In general, as long as you keep a consistent format, we can generally see where and why things change at a  glance. Then, we dig deeper into commit messages after.

If you're looking for some specific patterns, you might consider using something like [Conventional Branch](https://conventional-branch.github.io/). It'll give you a baseline of understanding some context for each branch.

You can even add the context of your task management provider or release process, like:

```
feature/TICKET-123-short-description
bugfix/TICKET-456-issue-description
hotfix/TICKET-789-critical-fix
release/v1.2.3
```

Having clear patterns for naming branches will help everyone understand the higher level context when trying to understand the graph of changes to the repo. As AI and LLM tools expand their context, your branch names might even give them extra context, too.

If you want to enforce specific branch naming conventions, you can add something to your CI/CD pipelines such as this [GitHub Action](https://github.com/marketplace/actions/github-repo-branch-naming-policy-action). You can see an example of it's usage [here in this repo](./.github/workflows/branch-naming.yaml).

## Git Hooks

This might be the most controversial part of this document because devs tend to feel very strongly about git hooks.

If you are unfamiliar with git hooks, they are shell scripts that run before or after certain git commands are run on the devs local machine. There are quite a few hooks available. You can find a full list in the [git documentation](https://git-scm.com/docs/githooks), but here are a few of the most common:

- `pre-commit`
- `pre-merge-commit`
- `prepare-commit-msg`
- `post-checkout`
- `pre-push`

The reason you will find that developers have strong opinions about hooks is that they can tend to get in the way of a devs flow state. Often it relates to how much time is spent in the hook. You probably don't want to run your entire test suite on a `pre-commit` hook, but running all local tests and linting in a `pre-push` hook can help prevent clogging your CI/CD pipeline with premature runs. However, something simple like linting and/or auto-formatting can make a lot of sense inside of a `pre-commit` hook to make sure the commits are in a more complete state when made since those steps tend to run very quickly.

Things you might consider adding hooks for include:
- Linting and static analysis
- Formatting
- Commit message validation
- Testing
- Verifying commit signing

In general, put yourself in the shoes of your devs and try not to get in their way while still providing value and saving them time.

## Commit Messages

There are a lot of opinions about how commit messages should be formed. One of the more universal opinions is that the tense of the commit message should be Imperative, present tense. This means "change" rather than "changes" or "changed".

One way to think about it is to substitute the message into this sentence: "The purpose of the commit is to _______".

One more thing to consider is adding the relevant ID from your issue tracking or project management solution. This is especially useful for tools that can generate autolinks out to the source of the ID to add extra context in places like your IDE.

A great [GitHub Gist](https://gist.github.com/janderssonse/1e65139ebcfb1a1bc6f04e877c2c60f2) exists that covers more of this information. However, you might consider using a more formal specification called [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

### Conventional Commits

This specification originates from the AngularJS team. It uses a set of specific keywords to signal the scope of a commit within the first word. Then, the rest of the commit adds context and detail. Here are some examples:

- `feat: add new widgets page`
- `fix: add widget to current list after creation`
- `docs: add documentation for widgets`

Using a convention like this can help you automate some of the more tedious parts of the release process, such as generating changelogs via [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog). You can also automate changing your semver version using [semantic-release](https://github.com/semantic-release/semantic-release) or [https://github.com/conventional-changelog/standard-version](https://github.com/conventional-changelog/standard-version). 

## Pull Requests

The basics of a good PR are a solid title and description. The title should be clear and communicate the general reason for the PR. You might want to include the issue or task ID related to the change. With a specific format, you can even automate changing the status of issues or tasks based on the PR being created and completed. This saves your devs valuable time by reducing the amount of "ClickOps" associated with project management which can also help prevent unnecessary context switching.

In more rigid environments and open source projects, you might want to take it one step further and use a pull request template. These are enforced at the hosting provider level such as GitHub.

GitHub has some [basic documentation](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository) for creating Pull Request templates.

While that documentation page shows how to create a PR template, it doesn't go very deep into what kinds of templates you might want to make. For that, there is a very good [collection of example templates](https://github.com/stevemao/github-issue-templates/).

Some of our favorites have been copied to this repo and can be found in the [.github/PULL_REQUEST_TEMPLATES](./.github/PULL_REQUEST_TEMPLATES) directory of this repo. Adding things like the [checklist template](./.github/PULL_REQUEST_TEMPLATES/checklist.md) to your repo can ensure that contributors are aggreeing to your contribution guidelines as well as make sure they aren't forgettting key bits of context.

## License

Copyright 2025 GitKraken

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
