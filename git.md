_All working directories are full repositories_

#### config
`git config --global core.editor "vim"` set default editor to vim  

`init` Create an empty git repository or re-initialize an existing one. Running in an existing repository is safe, nothing is overwritten, though the command can be used to move to another location. When this is done, a text file with the new path is placed in the current directory as a symbolic link to the new location.

`add` Add contents (files) to the index (snapshot of the working tree) staging them for the next commit. Only changes to the time of the add will be part of a commit. Further changes have to be added again.

`status` Displays path differences between index and HEAD commit.

`log` to see history

`log --pretty=oneline` for concise history

Further examples:  

```
git log --pretty=oneline --max-count=2  
git log --pretty=oneline --since='5 minutes ago'
git log --pretty=oneline --until='5 minutes ago'
git log --pretty=oneline --author='Michael Day'
```

#### branching

`git branch` list branches

#### rebase  

##### master
```
git checkout master
git pull
git checkout my-branch
git rebase master
git push origin -f my-branch
```

##### interactive
First, start interactive rebase. In this example, we are squashing the last two commits into one.  
`git rebase -i HEAD~2` 
  
This will load the interactive editor in VIM.  

`pick` the first commit in the list and `squash` the others - don't worry about the message. After we save this first "file" using VIM, we will immediately be taken to a second "file" where we can revise the messages for our included commits to be sure there is sufficient notes on the history.  

Once the rebase is complete, `git push origin -f my-branch`.

#### remote
`git remote -v` to see repositories whose branches are being tracked.

#### stash

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


***
bibliography  
https://git-scm.com/book/en/v2  
https://git-scm.com/docs  
http://ndpsoftware.com/git-cheatsheet.html  