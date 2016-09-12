#### 0_misc

`$?` Exit status  
`read` takes user input and assigns it to `$REPLY` by default  
`read -p "A proper prompt > " myvar` would output the prompt, and store the typed value into `$myvar`

#### DKIM  

Domain Keys Identified Email. A digital signature attached to each email validated against a public key.  
`host -t TXT dkimrecord`  

#### DMARC  

Domain-based Message Authentication, Reporting, and Conformance. To check use `dig txt _dmarc.somedomain.tld` used to tell the ESP what to do when the SPF or DKIM fails.

#### DNS

`whois domain.com`  
then, using the NS  
`nslookup domain.com NS-server` and  
`host domain.com NS-server`  

#### find
`find ~/path/to/start/from -name pattern` where pattern is the name or partial name (* / ?) of the file

#### gpg  
`gpg --list-keys`  to get see what keys are on a system  
`gpg --export > all.gpg` to get all keys on key ring  
`gpg --import > all.gpg` to import that key set into another system  
`gpg -r {key_id} -e {file_name}` encrypt a file (adds .gpg to the end of the file name to name the new file)   

#### ls
```
-c # use time when last changed for sorting (-t) or long printing (-l)  
-F # / directory * exe @ symbolic = socket % whiteout | FIFO  
-G # colorized  
-h # unit suffixes  
-l # long format  
-R # recursively list sub-directories encountered  
-r # reverse order  
-S # sort by size  
-t # sort by time modified  
-u # sort by time of last access  
-U # sort by time of file creation  
```

#### redirect  
`ls -al > directory_list.txt` file listing directory contents  
`ls > text.txt 2>&1` both std and err as `2>&1` redirects stderr to stdout

#### rsync  
`rsync -a file_to_send.txt username@server:~/path/if/desired`  

#### sftp  

`get filename.txt` transfers the file to the directory you logged into the sftp server from  

#### SPF  

Sender Policy Framework.  TXT records published on DNS that list hosts considered legit.  
`nslookup -type=txt domain.com`.  

#### source  

`source FILENAME [arguments]`  loads functions files  
For example, we may wish to `source ~/.profile`  re-load the profile after adding a new alias to our `.profile`.  

#### ssh  

`ls -al ~/.ssh` list present keys (if any)  


#### tmux  
`tmux ls` show sessions  
`tmux new -s session-name` new session  
`tmux a -t session-name` attach to a session  
`tmux detach`  detach from the session you are in  
`tmux kill-session -t session-name` end session entirely  
`killall tmux` end all sessions  

#### wc
`wc -l life_the_universe_and_everthing.sh` ideally this would return 42, as would running it :P   

### The real misc. debris...

#### hipchat

`/code import this` an effective way to see if your chat mate is a pythonista  
`/topic all the things` set room topic to "all the things"  
`/away coffee` set status to away with message of "coffee" see also `/available caffeinated` & `/dnd shaky`  
`s/ fucked/borked` look smart and/or cya  
`/me has left the building, following Elvis` mock announcements  
