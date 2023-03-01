
---
title: Git Documentation
tags:
  - Git
  - Commands
categories:
  - Git
date: 2016-09-13 16:13:32
---

<ul>
  <li>[--set-upstream](#--set-upstream)</li>
  <li>[How to undo last commit in Git?](#how-to-undo-last-commit-in-git?)</li>
  <li>[How would you skip a git hook?](#how-would-you-skip-a-git-hook?)</li>
  <li>[Save uncommitted changes with git stash](#save-uncommitted-changes-with-git-stash)</li>
  <li>[Navigate git command pager output with Unix less command](#navigate-git-command-pager-output-with-unix-less-command)</li>
  <li>[View commit history with git log](#view-commit-history-with-git-log)</li>
  <li>[Compare file changes with git diff](#compare-file-changes-with-git-diff)</li>
  <li>[Show who changed a line last with git blame](#show-who-changed-a-line-last-with-git-blame)</li>
  <li>[Use semantic versioning with git tag](#use-semantic-versioning-with-git-tag)</li>
  <li>[Clean up commits with git rebase](#clean-up-commits-with-git-rebase)</li>
  <li>[Diagnose which commit broke something with git bisect](#diagnose-which-commit-broke-something-with-git-bisect)</li>
  <li>[Run scripts on git events with git hooks](#run-scripts-on-git-events-with-git-hooks)</li>
  <li>[Configure global settings with git config](#configure-global-settings-with-git-config)</li>
  <li>[Configure global settings with git config](#configure-global-settings-with-git-config)</li>
  <li>[Remove all unnecessary git tracking with a global .gitignore file](#remove-all-unnecessary-git-tracking-with-a-global-.gitignore-file)</li>
</ul>

## --set-upstream

    git branch --set-upstream <remote-branch>

sets the default remote branch for the current local branch.

Any future git pull command (with the current local branch checked-out),
will attempt to bring in commits from the <remote-branch> into the current local branch.

One way to avoid having to explicitly do --set-upstream is
to use the shorthand flag -u along-with the very first git push as follows

    git push -u origin local-branch

This sets the upstream association for any future push/pull attempts automatically.
For more details, checkout this [detailed explanation about upstream branches and tracking][1].

---

  To avoid confusion, recent versions of git deprecate this somewhat ambiguous `--set-upstream` option in favor of a more verbose `--set-upstream-to` option with identical syntax and behavior `git branch --set-upstream-to <remote-branch>`.

[Rules are different for git push and git pull][2].

## How to undo last commit in Git

```bash
$ git commit -m "Something terribly misguided"              (1)
$ git reset HEAD~                                           (2)
<< edit files as necessary >>                               (3)
$ git add ...                                               (4)
$ git commit -c ORIG_HEAD                                   (5)
```

1. This is what you want to undo
2. This leaves your working tree (the state of your files on disk) unchanged but undoes the commit and leaves the changes you committed unstaged (so they'll appear as "Changes not staged for commit" in git status and you'll need to add them again before committing). If you only want to add more changes to the previous commit, or change the commit message1, you could use git reset --soft HEAD~ instead, which is like git reset HEAD~ but leaves your existing changes staged.
3. Make corrections to working tree files.
4. git add whatever you want to include in your new commit.
5. Commit the changes, reusing the old commit message. reset copied the old head to .git/ORIG_HEAD; commit with -c ORIG_HEAD will open an editor, which initially contains the log message from the old commit and allows you to edit it. If you do not need to edit the message, you could use the -C option instead.

***

Note, however, that you don't need to reset to an earlier commit if you just made a mistake in your commit message. The easier option is to git reset (to unstage any changes you've made since) and then ``git commit --amend``, which will open your default commit message editor pre-populated with the last commit message.

Beware however that if you have added any new changes to the index, using commit --amend will add them to your previous commit.

Reference link [here from stackoverflow][3] and [here from git][4].

## How would you skip a git hook

I have found some scenerarios where linters did not work correclty, and for instance I had to bypassed them.

Below option bypasses the pre-commit and pre-push.

    git commit --no-verify
    git push --no-verify

See also [githooks](https://git-scm.com/docs/githooks).

## Save uncommitted changes with git stash

Sometimes when we are working we need a way to pause and switch gears to deal with something more critical; often when this happens we aren't ready to create a ``git commit``; instead, we can use ``git stash`` to save our uncommitted changes locally, switch branches and fix the critical issue, switch back to our incomplete feature, and finally run ``git stash apply`` to get our unfinished changes back into our branch without affecting the rest of the codebase. Below it shows a real world example of doing this with a critical bug.

```bash
# Create a new feature branch.
git checkout -b feature/months

# Do Changes.
touch feature.js
vim feature.json

# ########################################
# Now we have to fix very important hotfix.
# ########################################

# Save uncommitted changes.
git add -A

# Save changes temporarily
git stash

# Saved working directory and index state WIP on months...
# And the HEAD goes back the previous commit.

# go to fix a critical issue and fix it
git checkout critical-issue

....

# When done, go back to the original branch
git checkout feature/months

# Get uncommitted changes
git stash apply

# Can get CONFLICTS, and they can be fixed as normal similar when merging.
```

## Navigate git command pager output with Unix less command

When using a git command that can have a large amount of output (like ``git log``, ``git diff``, or ``git blame``), Git opens the command output in our terminal "pager"; on most modern Unix-based systems, the default pager will be "[less](https://en.wikipedia.org/wiki/Less_(Unix))". Learning a few less commands will help us deal with this git command output that opens in the pager. Below it shows some of the most useful of the less commands:

`q` (quit), `j` (down), `k` (up), `Ctrl f` (forward), `Ctrl b` (backward), `/{search}` (search), and `n/N` (next/previous search result).

It covers some of the most critical less commands; there are more commands available. A good chunk of the commands (and "motions") of the Unix pagers are also used by vi (or vim) and other Unix programs.

## View commit history with git log

It's often helpful to view the history of a code project; with Git, we can use the ``git log`` command to view all commits in our repo. This lets us view information about each commit like the commit id (for use in other git commands), author, author's email, and commit message. We can format the git log commit output to display more or less information or filter to specific commits using ``git log {arguments}``.

```bash
git log {arguments}
# Terminal page
```

## Format commit history with git log arguments

When running the `git log` command, we can pass in options as arguments to _format_ the data shown for each commit.
Below it shows how to use the `oneline`, `decorate`, `graph`, `stat`, and `p` options with `git log`.

```bash
git log --oneline # Condensed info.
git log --decorate # All references.
git log --graph
git log -p # patch changes made in each commit.
git log --stat # Insertion and deletions per commit.
# compose options.
git log --online --graph
git log --stat --online
```

## Filter commit history with git log arguments

It will walk through using a bunch of options to filter our `git log` commits to a more meaningful set (`-n`, `--after`, `--before`, `--author`, `--grep`, `-S`, `-G`, `--no-merges`, `{ref}..{ref}`, {`files}`). We will also show how all of the formatting and filtering options can be composed together to query exactly what you are looking for in your commit history.

### Git log examples

```bash
git log -3 # 3 most recent commits.
git log --after="yesterday" # Now and yesterday.
git log --after="30 minutes ago"
git log --after="last tuesday"
git log --after="last week"
git log --after="2 weeks aog"
git log --after="3-15-16"
git log --after="3/15/16" --before="yesterday" # Commit between 3/15/16 and yesterday.
git log --since="3/15/16" --util="yesterday" # Are aliases.
git log --author="Mark" # Even emails.
git log --author="Mark\|jane" # Can be uses reg expressions.
git log --grep="copyright\|MIT"
git log -S"Math" # Code with Math
git log -p -S"Math" # Code with Math, see changes
git log -p -GMath\|Random # Reg exp.
git log -i # Ignore capitals
git log --no-merges # No committed merged changes.
git log master..cool-feature # Commits between.
git log LICENSE.md README.md # Only commits for a file(s).
git log -3 -i --author="pmagas" README.md
git log -S"Math" --after="2 months ago" --oneline --stat
```

## Compare file changes with git diff

It can be helpful to see the changes between two sets of code; `git diff` lets us do this by comparing two Git references and outputting the differences between them. Below it shows how to use `git diff` along with the `--stat`, `--cached`, `HEAD`, `origin/master`, `file(s)/dir(s)` options.

``git diff``: Show changes between two references; by default it uses the last commit, and the current working directory.

## Practical examples for git diff

```bash
git diff # Check what exa has changed.
git diff --stat # Diff with stats. Shows count lines have been modified.
git diff --cached # Show diff between the working directory and the staging area.
gid diff HEAD # To view all uncommitted changes, compares working directory, staging area with the last commit.
git diff {branch} # Branch name.
git fetch
git diff origin/master # Show all changes locally that they haven't been merged in the remote master branch.
 # By default uses all resources.
git diff origin/master getRandomString.js # Only diff of an specific file(s).
```

## Show who changed a line last with git blame

When working on a file, we often want to know who made certain changes last; we can use git blame to see details about the last modification of each line in a file. Below it shows and example of using `git blame` to see who made the last change on a line in a file, and then we use the output of `git blame` to use in other tools like `git log` to see the full context of why the change was made and what other parts of the code base were effected at the same time as the line from `git blame`.

### Practical example for git blame

```bash
git blame README.js
^15eeb90 (Pablo Magas 2016-09-14 06:29:56 +1200  1) ## Setup
^15eeb90 (Pablo Magas 2016-09-14 06:29:56 +1200  2) Get the application code cloning the git repository and installing all the dependencies.
....
# It says commit Id, who and when the change was done.
# We can see the log for specific commits.
git log 15eeb90 -p
```

## Use semantic versioning with git tag

Using `git tag` we can create references to commits that are immutable; this is usually used for making public releases. Below show how to use `git tag` and go over common Semantic Versioning (AKA semver) conventions.

Create references to a commit that can be changed.

### Practical examples with git tag

```bash
git tag v1.0.0 # Create tag with the label v1.0.0.
git tag
v1.0.0
git tag v2.0.0
git tag
v1.0.0
v2.0.0
git push --tags # Add tags to the remote repository.

git tag -a v2.0.1 -m "Some message" # Annotate to provide more detail.
git tag -a v2.0.1
-
-
#
```

1 - Major release, breaking code changes.
0 - Minor release, no breaking code changes, new functionality and maybe some bug fixes.
0 - Patch release, small bug fixes.

## Clean up commits with git rebase

Sometimes its nice to clean up commits before merging them into your main code repo; below it goes over using `git rebase` to `squash` commits together and then rename the condensed commit message.

### Practical examples using git rebase

```bash
git status

# E.g we have 6 commits without been pushed.
git fetch
git log origin/master.. # Compare the master branch with our local directory (branch).

git rebase -i  origin/master # -i: interactive

pick 1 # Original
s 2    # Changed pick to s.
s 3    # Changed pick to s.
s 4    # Changed pick to s.
s 5    # Changed pick to s.
s 6    # Changed pick to s.
# squash = use commit, but meld into previous commit.s
:x
#  This is a combination of 6 commits.

:x
Successfully rebased and updated refs/heads/master.

git status
Only 1 commit with all messages combined.

git log --oneline

# Maybe you committed a mistake, then you can abort
git rebase --abort
```

git rebase It is *DESTRUCTIVE*, change the git history, we shouldn't use rebase in code already pushed in the master branch.

## Diagnose which commit broke something with git bisect

Sometimes you find a bug in your project that has been around for a while without being noticed; it can be hard to track down where that bug was introduced and why just by searching through logs and diffs. Git has a slick tool called `git bisect` that can be used to find out which commit introduced problem in our code - it creates a binary search where the programmer can mark each search commit as `good` or `bad`; by the end of the bisect, Git shows you exactly which commit introduced the issue. Below it walks through an example of using `git bisect` from start to finish.

### Practical examples using git bisect

```bash
(git-documentation) git bisect start
(git-documentation|BISECTING) # Then BISECTING.
(git-documentation) npm test # Check the code is broken.
(git-documentation) git bisect bad # Mark as bad commit.
(git-documentation) git log --oneline # Find commit working properly.
(git-documentation) git log good 105e7cb
# Then a binary search of our commits between the good and bad reference and checks between the two.
(git-documentation) npm test # Check the code is broken again, it fails.
(git-documentation) git bisect bad
(git-documentation) npm test # Check the code is broken again, it passes.
(git-documentation) git bisect good
# Then the commit with error arises.
(git-documentation) git bisect reset # To come back the normal git state.

```

## Run scripts on git events with git hooks

Git lets us run scripts on git events like `pre-commit`, `pre-rebase`, `post-commit`, `post-merge`, `post-checkout`, etc. You can do this by adding an executable file to the `./git/hooks` directory which has a name matching the git hook name. Below it walks through this process by setting up a `pre-commit` hook which runs our `npm test` and `npm run lint` npm scripts to ensure we don't have any failing tests or lint errors before committing

### Practical examples using hooks

```bash
cd .git
ls -a hooks/
applypatch-msg.sample  fsmonitor-watchman.sample  pre-applypatch.sample  prepare-commit-msg.sample  pre-rebase.sample   update.sample
commit-msg.sample      post-update.sample         pre-commit.sample      pre-push.sample            pre-receive.sample

# Created locally
touch hooks/pre-commit
#!/bin/bash
npm test && npm run lint
chmod +x hooks/pre-commit
```

### Configure global settings with git config

You can set up global "[git config](https://git-scm.com/docs/git-config)" (`~/.gitconfig`) settings that apply to all git projects on your system. We then add our own git config settings: username, email, editor, and git aliases.

### Practical examples using git config

```bash
# Create alias
git config --global user.name 'Jane Doe'
git config --global alias.graph 'log --graph --online'
git config --global core.editor vim

# Get output of git config list.
git config --list
```

## Remove unnecessary git tracking with .gitignore files

Most projects have automatically generated files or folders from the operating system, applications, package managers etc. Usually, we don't want to include these types of things in our remote repos because they can clutter the git history/storage and are not applicable to everyone that works on the project. Below it shows how to create a `.gitignore` file to ignore files and folders from being tracked by git.

### Practical examples using .gitignore

```bash
touch .gitignore
vim .gitignore
# Do not track these files.
.DS_store
Thumbs.db
.identical
*.sublime-workspace
node_modules
npm-debug.log
*.png
cache
```

## Remove all unnecessary git tracking with a global .gitignore file

If you regularly use code editors, GUI tools or other programs that automatically create files and folders, you may want to set up a global `.gitignore` file which will apply to every repo on your machine. Below it shows how to do that by creating a `.gitignore_global` file with the dotfiles in our `~/` root directory, and then link it to all git repos using our global `.gitconfig`.

```bash
touch ~/.gitignore_global # Any but recommend by git.
vim ~/.gitignore_global
.DS_store
.directory
node_modules

git config --global core.excludesfile ~/.gitignore_global
```

## References

[1]: http://stackoverflow.com/a/10002469/319204
[2]: http://longair.net/blog/2011/02/27/an-asymmetry-between-git-pull-and-git-push/
[3]: http://stackoverflow.com/questions/927358/how-to-undo-last-commits-in-git
[4]: https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things
