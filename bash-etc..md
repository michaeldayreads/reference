### bash  

#### find
`find ~/path/to/start/from -name pattern` where pattern is the name or partial name (* / ?) of the file

#### redirect  
`ls -al > directory_list.txt` file listing directory contents  
`ls > text.txt 2>&1` both std and err as `2>&1` redirects stderr to stdout

#### source  

`source FILENAME [arguments]`  loads functions files  
For example, we may wish to `source ~/.profile`  re-load the profile after adding a new alias to our `.profile`.  

### sftp  

`get filename.txt` transfers the file to the directory you logged into the sftp server from


### DNS

`whois domain.com`  
then, using the NS  
`nslookup domain.com NS-server` and  
`host domain.com NS-server`  

## email

Always get the headers  

### SPF  

Sender Policy Framework.  TXT records published on DNS that list hosts considered legit. Check using `nslookup -type=txt domain.com`.  

### DKIM  

Domain Keys Identified Email. A digital signature attached to each email validated against a public key.

### DMARC  

Domain-based Message Authentication, Reporting, and Conformance. To check use `dig txt _dmarc.somedomain.tld` used to tell the ESP what to do when the SPF or DKIM fails.

