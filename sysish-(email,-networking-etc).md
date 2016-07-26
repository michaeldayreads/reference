Always get the headers  
nslookup -type=txt domain.com  

whois domain.com  
then, using the NS  
nslookup domain.com NS-server and  
host domain.com NS-server  