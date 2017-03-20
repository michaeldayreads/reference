_All working directories are full repositories_

# organized by command (no specific order)

## add

`add` Add contents (files) to the index (snapshot of the working tree) staging them for the next commit. Only changes to the time of the add will be part of a commit. Further changes have to be added again.

## config

`git config --global core.editor "vim"` set default editor to vim  

## diff  

`git diff branch_1 branch_2` compare two branches  
`git diff branch_1 branch_2 path/to/file_of_interest.txt` compare a file between two branches

## init

`init` Create an empty git repository or re-initialize an existing one. Running in an existing repository is safe, nothing is overwritten, though the command can be used to move to another location. When this is done, a text file with the new path is placed in the current directory as a symbolic link to the new location.

## status

`status` Displays path differences between index and HEAD commit.

## log

`log` to see history

`log --pretty=oneline` for concise history

`git log --date=local --author="<person of interest>"` to see what's been done & when (standup log hack)  

Further examples:  

```
git log --pretty=oneline --max-count=2  
git log --pretty=oneline --since='5 minutes ago'
git log --pretty=oneline --until='5 minutes ago'
git log --pretty=oneline --author='Michael Day'
git log --graph --color --oneline --decorate
```

## branch

`git branch` list branches  
`git branch -r` list remote branches  
`git branch -d <branch to delete>`  
`git branch -D <branch to delete>` shorthand for `git branch -d --force <branch to delete>`  
`git branch -m <old_name> <new_name>` to rename a branch you are not on  
`git branch -m <new_name>` to rename current branch  

## stash

`git stash` To stash things for later  
`git stash list` to see the stash "stack"  
`git stash show -p [stash@{n}]` essentially a diff  
`git stash apply`  to apply the last set of stashed changes  
`git stash apply stash@{n}` to apply the nth set  
`git stash apply [stash@{n}] --index` apply and stage as staged at stash   
`git stash drop [stash@{n}]` remove nth set (or last if omitted)  
`git stash pop [stash@{n}]` apply and remove nth set (or last if omitted)  
`git stash save "a more useful name"` stash with the useful name showing in `git stash list`  
`git stash clear` to remove all items from the stash **caution**  

# by concept or use pattern

## cherry-pick

Cherry pick is a method to apply a commit - or set of commits - and create a new commit for each. One example is if your team has release branches in addition to a master branch. As each member of the team works on fixes and features, all of those commits are merged to master. Then, depending on timing and completeness relative to releases, the commits associated with a given feature can be "cherry-picked" into the feature branches. 

This produces a history on the feature branches that tracks the history seen on the master branch.

As always, there are as many ways to implement cherry-pick as there are teams that use it, but here is one example:

`git cherry-pick -x -m 1 <commit-id>`

* The `-x` options instructs git to include a "cherry-picked from ..." bread crumb in the log.
* the `-m 1` instructs git which parent number to choose as mainline.

## ignore

`vim .git/info/exclude`  to ignore items in a local repo where the ignores themselves are not committed to the repo.  

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
  
This will load the interactive editor in VIM.  

`pick` the first commit in the list and `squash` the others - don't worry about the message. After we save this first "file" using VIM, we will immediately be taken to a second "file" where we can revise the messages for our included commits to be sure there is sufficient notes on the history.  

Once the rebase is complete, `git push origin -f my-branch`.

## remote and upstream  

`git remote -v` to see repositories whose branches are being tracked.

`git remote add upstream <url>` to add an upstream

`git remote set-url origin <new url>` to update an origin (or upstream) following a name change  

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


```
git checkout master
git pull upstream master
git push origin master
git checkout my-branch
git rebase master
```
