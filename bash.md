### 0_misc 

#### redirect  
`ls -al > directory_list.txt` file listing directory contents  
`ls > text.txt 2>&1` both std and err as `2>&1` redirects stderr to stdout  

#### sftp  

`get filename.txt` transfers the file to the directory you logged into the sftp server from  

#### SPF  

Sender Policy Framework.  TXT records published on DNS that list hosts considered legit.  
`nslookup -type=txt domain.com`.  

#### ssh  
`ls -al ~/.ssh` list present keys (if any)  

#### interactive
>`clear && ls -lG` demo of multiple commands on one line using `&&`  

#### programming  
>`$?` Exit status  
>`read` takes user input and assigns it to `$REPLY` by default  
>`read -p "A proper prompt > " myvar` would output the prompt, and store the typed value into `$myvar`  

#### reverse-i-search
>`CTRL-R` to search for a command in the history - e.g. `CTRL-R` `ssh` `CTRL-R` `CTRL-R` to find the third match >then `CTRL-Shift-R` to go back to the second.  

>Add a comment to tag things: `command #tag` allows `CTRL-R` `#tag` to find those commands so tagged.  

#### stash
>`CTRL-A` to get to the start of your line  
>`CTRL-K` to stash it  
>`CTRL-Y` to yank it  

#### nginx
> `/etc/init.d/nginx status`  
> `/etc/init.d/nginx start`  
> `/etc/init.d/nginx stop`  
> `/etc/init.d/nginx restart`  

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

# commands

## APT
> `apt-get update`
> resynchronize the package index files

`apt-get install foo`
> install foo

## brctl (bridge control - ethernet bridge admin)
`brctl show` list network bridges

## chmod  

Change file mode bits.

`chmod +x script.sh`  make `script.sh` executable  

### Symbols  
Multiple can be given, separated by commas.

#### rwxXst
`r` read  
`w` write  
`x` execute  
`X` execute or search only if file is a directory or already has execute permission for some user [?]    
`s` set user or group ID on execution [?]  
`t` restrict deletion flag [?]  

#### ugoa  
`u` _user_ who owns it  
`g` file's _group_  
`o` _other_ users not in the files group  
`a` _all_ users  

## find
`find ~/path/to/start/from -name pattern` where pattern is the name or partial name (* / ?) of the file

## gpg  
`gpg --list-keys`  to get see what keys are on a system  
`gpg --export > all.gpg` to get all keys on key ring  
`gpg --import > all.gpg` to import that key set into another system  
`gpg -r {key_id} -e {file_name}` encrypt a file (adds .gpg to the end of the file name to name the new file)   

## history

`history | grep command-of-interest`  

```
270 blah-blah-blah  
271 command-of-interest  
272 blah-blah-blah
```

Then use the `!n` event designator to target the line you want to repeat...

`!271` 

## ls
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

## rsync  
`rsync -a file_to_send.txt username@server:~/path/if/desired`  

## source  

`source FILENAME [arguments]`  loads functions files  
For example, we may wish to `source ~/.profile`  re-load the profile after adding a new alias to our `.profile`.  

## uptime  
`uptime` to see how long server has been running, users, load averages for 1,5 and 15 minutes  

## wc
`wc -l life_the_universe_and_everthing.sh` ideally this would return 42, as would running it :P   

### The real misc. debris...

### vagrant
`vagrant ssh -- -A -v`