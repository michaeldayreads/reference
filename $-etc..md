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

#### redirect  
`ls -al > directory_list.txt` file listing directory contents  
`ls > text.txt 2>&1` both std and err as `2>&1` redirects stderr to stdout

#### sftp  

`get filename.txt` transfers the file to the directory you logged into the sftp server from  

#### SPF  

Sender Policy Framework.  TXT records published on DNS that list hosts considered legit.  
`nslookup -type=txt domain.com`.  

#### source  

`source FILENAME [arguments]`  loads functions files  
For example, we may wish to `source ~/.profile`  re-load the profile after adding a new alias to our `.profile`.  

#### tmux  
`tmux ls` show sessions  
`tmux new -s session-name` new session  
`tmux a -t session-name` attach to a session  
`tmux detach`  detach from the session you are in  
`tmux kill-session -t session-name` end session entirely  
`killall tmux` end all sessions  

