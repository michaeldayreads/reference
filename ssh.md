# quick ref  

`eval "$(ssh-agent -s)"`  use bash eval to invoke command substitution to invoke the generation of shell agent commands which are then evaluated to activate the agent to hold the private keys. See `man ssh-agent` for further information.  

# ssh  

## common options  
`-o` method to specify options not available via other command-line flags, using the format one would use for the configuration file, e.g `ssh -o UserKnownHostsFile=/dev/null`  

# ssh-add  

`ssh-add -l` list keys on current agent  
`ssh-add ~/.specify_key_file` add specified key, in this case from default file path  
