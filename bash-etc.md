## bash  

#### redirect  
`ls -al > directory_list.txt` file listing directory contents  
`ls > text.txt 2>&1` both std and err as `2>&1` redirects stderr to stdout



##svn  

**Check out an earlier revision than head**  
`svn co -r 2718 file:///var/svn/repo_or_file /target/path`