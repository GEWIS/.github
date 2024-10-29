# Contributing to GEWIS

We would love for you to contribute to GEWIS systems and make them even better than they are today! You don't have to be an ABC member or an experienced software engineer — everyone is welcome.

This document guides you on how to contribute to software within GEWIS and points out some tips and best practices so that you can write better code that can more easily be accepted.

This document is a general and overarching guide — the actual project repositories themselves might include more case-specific tips on how to contribute to them, so make sure to read those as well.

## Language, spelling, and grammar

All documents, code, and relevant documentation should be in English. Given that you are most likely studying at the university in English, this should not be a problem. However, keep the following in mind:
- Use British English instead of American English.
- Write short sentences.
- Whenever possible, use the present tense.
- Whenever possible, use the active voice.

## Submitting a Pull Request (PR)

To contribute to a project, you can create a pull request, but make sure to consider the following guidelines before doing so:

1. Search the project's GitHub for an open or closed PR that relates to your submission. You don't want to duplicate existing efforts.

2. Be sure that an issue describes the problem you're fixing or documents the design for the feature you'd like to add. Discussing the design upfront helps to ensure that we're ready to accept your work.

3. Fork the relevant repo.

4. In your forked repository, make your changes in a new git branch:

   ```shell
   git checkout -b my-fix-branch main
   ```

   Make sure to name your branch `Feature` or `Fix`, followed by a descriptive name.

5. Write your patch, **including appropriate test cases**.

6. Commit your changes using a descriptive commit message that follows the [conventional commits standard](#commit). Adherence to these conventions is necessary because release notes are automatically generated from these messages.

   ```shell
   git commit --all
   ```

   Note: the optional commit `--all` command line option will automatically "add" and "rm" edited files.

7. Push your branch to GitHub:

   ```shell
   git push origin my-fix-branch
   ```

8. In GitHub, send a pull request to the corresponding project.

### Rebasing vs Merging

In general, we prefer to rebase rather than merge. Rebasing makes the history cleaner and easier to follow. The downside is that solving conflicts during a rebase can be more time-consuming than merging. For more information, see [this guide](https://www.freecodecamp.org/news/git-rebase-handbook/).

To rebase your branch on the main branch, you can use the following command:

```shell
git checkout my-fix-branch

git rebase main
```

This will start a rebase process that will reapply your changes on top of the main branch. IDEs like VSCode and JetBrains WebStorm have an interactive rebase feature that can help you resolve conflicts during the rebase process.

Make sure to force push your branch after the rebase process, since rebasing rewrites the history of your branch. Always use `--force-with-lease` and never `--force` when pushing to GitHub.

```shell
git push --force-with-lease origin my-fix-branch
```

### Reviewing a Pull Request

The project maintainers, most likely members of the ABC, reserve the right not to accept pull requests.

#### Addressing review feedback

If we ask for changes via code reviews, then:

1. Make the required updates to the code.

2. Create a fixup commit and push to your GitHub repository (this will update your Pull Request):

   ```shell
   git commit --all --fixup HEAD
   git push
   ```

   For more info on working with fixup commits, see the [git documentation](https://git-scm.com/docs/git-commit).

That's it! Thank you for your contribution!

##### Updating the commit message

A reviewer might often suggest changes to a commit message (for example, to add more context for a change or adhere to our [commit message guidelines](#commit)). In order to update the commit message of the last commit on your branch:

1. Check out your branch:

   ```shell
   git checkout my-fix-branch
   ```

2. Amend the last commit and modify the commit message:

   ```shell
   git commit --amend
   ```

3. Push to your GitHub repository:

   ```shell
   git push --force-with-lease
   ```

> **NOTE:**<br />
> If you need to update the commit message of an earlier commit, you can use `git rebase` in interactive mode.  
> See the [git docs](https://git-scm.com/docs/git-rebase#_interactive_mode) for more details.

#### After your pull request is merged

After your pull request is merged, you can safely delete your branch and pull the changes from the main (upstream) repository:

* Delete the remote branch on GitHub either through the GitHub web UI or your local shell as follows:

   ```shell
   git push origin --delete my-fix-branch
   ```

* Check out the main branch:

   ```shell
   git checkout main -f
   ```

* Delete the local branch:

   ```shell
   git branch -D my-fix-branch
   ```

* Update your local `main` with the latest upstream version:

   ```shell
   git pull --ff upstream main
   ```

## <a name="rules"></a> Coding Rules
To ensure consistency throughout the source code, keep these rules in mind as you are working:

* All features or bug fixes **must be tested** by one or more specs (unit-tests).
* All public API methods **must be documented**.

Note that not every repository has test, so this may differ per project.

## <a name="commit"></a> Commit Message Format

We follow the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/), which provides a standardised format for commit messages. Thi also enables automated tooling for releases. The commit message format is as follows:

```
<type>[optional scope]: <description>
```

Types include:
- `feat`: A new feature.
- `fix`: A bug fix.
- `docs`: Documentation changes.
- `style`: Code style improvements (e.g., formatting).
- `refactor`: Code changes that neither fix a bug nor add a feature.
- `test`: Adding or modifying tests.
- `chore`: Maintenance tasks, like tooling or configuration changes.

For example: `feat(user): add login functionality`

Also make note of the following:
* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize the first letter
* no dot (.) at the end