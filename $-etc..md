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

