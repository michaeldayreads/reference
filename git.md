# add

`add` Add contents (files) to the index (snapshot of the working tree) staging them for the next commit. Only changes to the time of the add will be part of a commit. Further changes have to be added again.

# `branch`

`git branch` list branches  
`git branch -r` list remote branches  
`git branch -d <branch to delete>`  
`git branch -D <branch to delete>` shorthand for `git branch -d --force <branch to delete>`  
`git branch -m <old_name> <new_name>` to rename a branch you are not on  
`git branch -m <new_name>` to rename current branch  

# `checkout`

Update file(s) in the working tree to match the state of those files in the SHA provided.

`git checkout -b local_branch upstream/fix-or-feature-branch` track remote branch

`git checkout --track upstream/branch_to_track` track an existing remote branch

## Update / Revert file(s)

Checkout is useful to revert a file to an earlier state or to copy changes from one branch to another for specific files.

`git checkout <SHA> path/to/file`  

```
git checkout source_branch
git log -1  # get the SHA
git checkout target_branch
git checkout <SHA> path/to/file
```
## Duplicate or Copy an Existing Branch to a New Branch

```
git checkout old
git branch new
```

OR

`git checkout -b new old

# `cherry-pick`

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

# `config`

`git config --global core.editor "vim"` set default editor to vim  
`git config --list`  see current config.

# `diff`

`git diff branch_1 branch_2` compare two branches  
`git diff branch_1 branch_2 path/to/file_of_interest.txt` compare a file between two branches
`git diff --name-only SHA1 SHA2` lists the files that changed
`git diff SHA name_of_file` as a drill down from `--name-only`

# `fetch`

`git fetch --all --prune` remove deleted branches  

# `init`

Create an empty git repository or re-initialize an existing one. Running in an existing repository is safe, nothing is overwritten, though the command can be used to move to another location. When this is done, a text file with the new path is placed in the current directory as a symbolic link to the new location.

# `ignore`

`vim .git/info/exclude`  to ignore items in a local repo where the ignores themselves are not committed to the repo.  

# `log`

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

## comparing branches

`git log foo/master ^bar/master`

Show what commits are in foo that are not in bar. 

# `merge`

# `mergetool`


# `push`

> hack to prevent pushing by accident: `git remote set-url --push origin no_push`


`git push <remote> source_branch:target_branch`

# `remote`

# `remote`

`git remote -v` verbose list of remotes
`git remote add any_name_you_like` adds a remote
`git remote rm any_name_you_like` removes a remote
`git remote add upstream <url>` to add an upstream
`git remote set-url origin <new url>` to update an origin (or upstream) following a name change  

# `show`

Details of an object (commit).

`git show <sha>`

`git show <sha> -s`  Suppress the diff, equivalent to `--no-patch`

# `status`

Displays path differences between index and HEAD commit.

# `stash`

`git stash` To stash things for later  
`git stash save "short descriptive name"` or you will have a cryptic name for the stash
`git stash list` to see the stash "stack"  
`git stash show -p [stash@{n}]` essentially a diff  
`git stash apply`  to apply the last set of stashed changes  
`git stash apply stash@{n}` to apply the nth set  
`git stash apply [stash@{n}] --index` apply and stage as staged at stash   
`git stash drop [stash@{n}]` remove nth set (or last if omitted)  
`git stash pop [stash@{n}]` apply and remove nth set (or last if omitted)  
`git stash save "a more useful name"` stash with the useful name showing in `git stash list`  
`git stash clear` to remove all items from the stash **caution**  


# `status`

Displays path differences between index and HEAD commit.

# `submodule`

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
