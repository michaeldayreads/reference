_All working directories are full repositories_

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

_stash_

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