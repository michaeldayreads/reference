# Useful Hacks and One liners

```bash
# Push to all remotes.
# Invoked as `git pushall`.
# From https://stackoverflow.com/questions/5785549/able-to-push-to-all-git-remotes-with-the-one-command
#
git config --global alias.pushall '!git remote | xargs -L1 git push --all'
```

# Commands

## `add` 

Add contents (files) to the index (snapshot of the working tree) staging them for the next commit. Only changes to the time of the add will be part of a commit. Further changes have to be added again.

## `branch`

`git branch` list branches  
`git branch -r` list remote branches  
`git branch -d <branch to delete>`  
`git branch -D <branch to delete>` shorthand for `git branch -d --force <branch to delete>`  
`git branch -m <old_name> <new_name>` to rename a branch you are not on  
`git branch -m <new_name>` to rename current branch  

### Converting a detached head to a branch

If you checkout a SHA, you will be in a detached head state. This is useful for looking around, but if you need to make changes or wish to name that SHA for ease of reference without creating a tag, best to create a branch.

```
git checkout <SHA>
git branch foo
git checkout foo
```

## `checkout`

Update file(s) in the working tree to match the state of those files in the SHA provided.

`git checkout -b local_branch upstream/fix-or-feature-branch` track remote branch

`git checkout --track upstream/branch_to_track` to check out a local copy of a remote branch and set the local copy to track that remote copy.

> Use `git branch --set-upstream-to remote/branch` to add or modify the remote branch that your local should track.

### Update / Revert file(s)

Checkout is useful to revert a file to an earlier state or to copy changes from one branch to another for specific files.

`git checkout <SHA> path/to/file`  

```
git checkout source_branch
git log -1  # get the SHA
git checkout target_branch
git checkout <SHA> path/to/file
```
### Duplicate or Copy an Existing Branch to a New Branch

```
git checkout old
git branch new
```

OR

`git checkout -b new old

## `cherry-pick`

Cherry pick is a method to apply a commit - or set of commits - and create a new commit for each. One example is if your team has release branches in addition to a master branch. As each member of the team works on fixes and features, all of those commits are merged to master. Then, depending on timing and completeness relative to releases, the commits associated with a given feature can be "cherry-picked" into the feature branches.

This produces a history on the feature branches that tracks the history seen on the master branch.

As always, there are as many ways to implement cherry-pick as there are teams that use it, but here is one example:

`git cherry-pick -x -m 1 <commit-id>`

-x adds a comment saying what commit it was picked from

-m specifies the mainline parent, from 1

A more complete statement of this example is:

```
git fetch --all                               # so that --ff-only is accurate
git checkout master
git merge --ff-only upstream/master
git log --oneline                             # find <sha> of interest, typically a merge commit
git checkout target_branch                    # typically a release branch, e.g 1.0-stable
git merge --ff-only upstream/target_branch    # just to be sure current
git cherry-pick -x -m 1 <sha>
git push origin target_branch:target_branch   # and then open a PR or MR
```

* The `-x` options instructs git to include a "cherry-picked from ..." bread crumb in the log.
* the `-m 1` instructs git which parent number to choose as mainline.

Another useful pattern is to combine two orthoganal changes that have been tested on separate branches:

```
git checkout fix-a                              # this branch fixes issue a, and we want to combine the fix for b into it
git log -10 fix-b                               # to find SHA for commit that fixes issue b
git cherry-pick <SHA for fix b>                 # now we have fix b on top of fix a; be mindful of time stamps and rebase as needed
```

## `commit`

The message has two parts: the [title](/terms/tbd?commit-title) which is the message up to the first blank line, and the rest of the message. The [title](/terms/tbd?commit-title) should be short - suggested less than 50 characters - and should summarize the changes in that commit. It is used throughout `log` and other subcommands/functions and should be written with thoughtful precision.


`git commit --amend --author "Corrected Name <corrected@email.com>"`

`git commit --date=format:relative:2.days.ago -m "Set _author_ commit time only."` To also have the GIT_COMMITTER_DATE the env variable has to be set for each commit, but often the author date is what you care about (e.g. the activity that shows on github).

## `config`

`git config --global core.editor "vim"` set default editor to vim.  Note that the `--global` flag must _precede_ arguments being set.  
`git config --list`  see current config.  
`git config --list --global` to see global config. Note, if none are set, an error is generated.  
`git config user.email "foo@baz.com"`  set email (for repo).  
`git config user.email` view email (for repo).  

## `diff`

`git diff branch_1 branch_2` compare two branches  
`git diff branch_1 branch_2 path/to/file_of_interest.txt` compare a file between two branches  
`git diff --name-only SHA1 SHA2` lists the files that changed  
`git diff SHA name_of_file` as a drill down from `--name-only`

To focus on changes smaller than lines:

```
git diff --word-diff <sha_or_file(s)_as_usual>              # word diff, in the bash or vim sense of word
git diff --word-diff-regex=. <sha_or_file(s)_as_usual>      # character diff using {+change+} notation
git diff --color-words=. <sha_or_file(s)_as_usual>          # highlights what changed directly, no additional markers
```


## `fetch`

`git fetch --all --prune` remove deleted branches  

## `init`

Create an empty git repository or re-initialize an existing one. Running in an existing repository is safe, nothing is overwritten, though the command can be used to move to another location. When this is done, a text file with the new path is placed in the current directory as a symbolic link to the new location.

## `ignore`

`vim .git/info/exclude`  to ignore items in a local repo where the ignores themselves are not committed to the repo.  

## `log`

Commit history

`log --pretty=oneline` for concise history

`git log --date=local --author="<person of interest>"` to see what's been done & when (standup log hack)  

Further examples:  

```
git log --pretty=oneline --max-count=2  
git log --pretty=oneline --since='5 minutes ago'
git log --pretty=oneline --until='5 minutes ago'
git log --pretty=oneline --author='Michael Day'
git log --graph --color --oneline --decorate
git log --grep=coverage
```

### comparing branches

Imagine that branch `foo` has one commit that `master` does not have.

`git log foo ^master`

Will show that one commit, as we are asking git 'what commits are in foo that are _not_ in master?'.

However, if we instead invoke:

`git log master ^foo`

The result will be empty, as there _are no commits in master that are not in foo_.


## `merge`

When merging - which is also the basis for `rebase`, `stash pop` and `stash apply` to keep `us` and `them` clear:

`us` = into and `them` = from


## `push`

> hack to prevent pushing by accident: `git remote set-url --push origin no_push`


`git push <remote> source_branch:target_branch`

## `remote`

`git remote -v` verbose list of remotes
`git remote add any_name_you_like` adds a remote
`git remote rm any_name_you_like` removes a remote
`git remote add upstream <url>` to add an upstream
`git remote set-url origin <new url>` to update an origin (or upstream) following a name change  

## `revert`

Use `git revert <sha>` to undo an earlier commit.

When reverting multiple commits, reverse the order so they get backed out in the right way.

That is:

```
<sha_second> foo
<sha__first> bar
```

would be reverted by invoking `git revert <sha_second> <sha_first>`

If there are conflicts, either the order you are specifying is incorrect or the scope of what you are looking to revert needs to be re-evaluated.

## `show`

Details of an object (commit).

`git show <sha>`

`git show <sha> -s`  Suppress the diff, equivalent to `--no-patch`

`git show <sha> --name-only`  Supress the diff, but show the files modified.  


## `status`

Displays path differences between index and HEAD commit.

## `stash`

`git stash <pathspec>` is a quick way to invoke `git stash push <pathspec>`, though using the more complete syntax can expose more options.

In practice, what often is most effective is:

```
git stash push -m "Describe changes" -- <pathspec>
```

The pathspec is optional, as just the `--` can be used to compare to head. Note that new files must be added. So another way to think of this workflow is;

```
git add <pathspec> ... <pathsepc>
git stash push -m "stash message" --
```

or

```
git add <pathspec> ... <pathsepc>
git stash push -m "stash message" -- <pathspec> ... <pathspec>
```

... in cases where there a files that are tracked and modifed, but not added that we don't want to stash and that we don't yet want to commit.

is an alternative to 

```
git add <pathspec> ... <pathsepc>
git commit -m "commit message"
```

This lets us leave uncommitted changes to files already tracked in a modified state for further changes before either stashing or committing them.

In both cases, anything not specifically added is left as changes in the working directory.


`git stash` To stash things for later.  
`git stash -p` To have git break what has changed into "hunks" and ask you what to do with each.  
`git stash -m "short descriptive name"` or you will have a cryptic name for the stash.  
`git stash list` to see the stash "stack".  
`git stash show -p [stash@{n}]` essentially a diff.  
`git stash apply`  to apply the last set of stashed changes.  
`git stash apply stash@{n}` to apply the nth set.  
`git stash apply [stash@{n}] --index` apply and stage as staged at stash.  
`git stash drop [stash@{n}]` remove nth set (or last if omitted).  
`git stash pop [stash@{n}]` apply and remove nth set (or last if omitted).  
`git stash clear` to remove all items from the stash **caution**.  


## `status`

Displays path differences between index and HEAD commit.

## `submodule`

`git submodule status`  
`git submodule sync`  
`git submodule update --init` for the first time...  
`git submodule update` on subsequent ones...  

to remove: [^so-1260748]
* delete section from `.gitmodules` or, if last one, remove the file
* delete section (if any) from `.git/config`
* `git rm --cached path_to_submodule` (no trailing slash)
* `rm -rf .git/modules/path_to_submodule`
* `git commit -m "removed submodule <name>"`


## `tag`

Mark a point (sha) in the commit history. 

A tag can be local or remote, simple or annotated.

A common use case is to tag a release.

A personal use case is to tag the sha a work in progress is forked from to simplify commands and automation by using the tag as a pointer to a sha.

```
git log -10                 #  find sha to use for commands like rebase and diff
git tag foo <sha>           #  attept to locally tag this sha as "foo"
git tag -d foo              #  to move the tag, first delete it
```

## `worktree`

An alternative to having multiple clones of the same repo on one host. Particularly useful for running tests, since you can have long running tests or multiple versions of tests running in the background or in parallel.

We'll use this as an example; we want to run tests on project `foo` -- lets say in a loop -- while we tinker with the test we think is problematic in another directory of the file structure. We could do this with git clone, but this requires the network, might be expensive, and it does not include the conflict avoidance that `git worktree` provides.

```
cd foo
git worktree add ~/.gwt/foo-test-0                  # Any path works. This example uses a `.gwt` directory to house worktrees.
                                                    # The last part of the slug will be created, the rest must already exist.
git worktree list                                   # Lists worktrees in a manner that makes cd simple, also shows sha/branch.
cd ~/.gwt/foo-test-0                                # If branch `foo-test-0` did not exist, it does now and we're on it. 
./start_tests.sh                                    # Run the tests. Now switch to another terminal and navigate back to foo.
```

The conflict avoidance is very helpful. In the original directory for `foo`, attempting to `git checkout foo-test-0` will fail. To manipulate that branch, you have to navigate to the directory of the working tree.

Use:
- `git worktree move <path/to/worktree/dir>` to move the files and keep git aware of them.
- `git worktree remove <path/to/worktree/dir>` to delete a worktree no longer being used.
- `git worktree prune` to clean up admin files.

^^^ refactored ^^^

by concept or use pattern
--------------------------

`git checkout -b local_branch upstream/fix-or-feature-branch` track remote branch

## reset hard to fix stuff

The usual warnings about using forks and staying off of master apply.

use `git log` or `git reflog` to find the sha of the commit you want to get back to, then:

`git reset --hard < SHA >`

Note that if you were attempting to rebase or otherwise merge when you mucked things up, you may need to `git merge --abort` or `git rebase --abort` as well.

## rebase branch changes into updated master  

```
git checkout master
git pull
git checkout my-branch
git rebase master
git push origin -f my-branch
```

### when there is an upstream

```
git checkout master
git pull upstream master
git checkout my-branch
git rebase master
git push origin  
```

## interactive rebase to squash commits  

First, start interactive rebase. In this example, we are squashing the last two commits into one.  
`git rebase -i HEAD~2`

To be more explicit, suppose we have the following `git log` entries:

```
f53648c WIP: data for example Michael Day Fri May 12 13:54:39 2017
08aabb4 Exceptions, testing, and tox Michael Day Fri May 12 13:52:46 2017
1d8284d Started python refactor, rename shell Michael Day Sun May 7 10:53:31 2017
```

We can use `git rebase -i 1d8284d` to "stand on top of" commit 1d8284d to perform our rebase. This has the same result (in this specific case) as `git rebase -i HEAD~2` and has the advantage of being more explicit.

Either method starts the interactive rebase in your default editor.  

The most common pattern has been to `pick` the first commit in the list and `squash` or `fixup` the others. This gives us the option of including/modifying the commit messages in the case of `squash`, or discarding those messages in the case of `fixup` After we save this first "file" using VIM, we will immediately be taken to a second "file" where we can revise the messages for our included commits to be sure there is sufficient notes on the history.  

Once the rebase is complete, `git push origin -f my-branch`.


## fork, rebase to origin, merge to upstream
```
git checkout master  
git pull upstream master
git push origin master
git checkout fix-or-feature-branch
git rebase -i HEAD~n # squash all of you WIP commits
git rebase master # and resolve any conflicts
git push -f origin fix-or-feature-branch:fix-or-feature-branch
```

# sources
https://git-scm.com/book/en/v2  
https://git-scm.com/docs  
http://ndpsoftware.com/git-cheatsheet.html  
[^so-1260748]: (https://stackoverflow.com/questions/1260748/how-do-i-remove-a-submodule#1260982)


```
git checkout master
git pull upstream master
git push origin master
git checkout my-branch
git rebase master
```
docker run --rm -it -v $PWD:$PWD docker-registry.pdbld.f5net.com/velcro/attributions-generator:master /usr/loc
al/bin/run-backends.sh $PWD
