## DNS

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
