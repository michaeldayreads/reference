# cli

## attach

`docker attach <name>`  



## build
`docker build -t tag -f /path/to/Dockerfile.special /path/to/context/for/commands/in/Dockerfile`  

> note that `-f` expects a file with a full path, even if `Dockerfile.special` is in the context specified in the build invocation.  

*Attach* to a running container with a shell tty  
>on host:  
>`docker exec -it <containerId> bash`  

*Copy* a file from a container to a host  
>on host:  
>`docker cp <containerId>:/path/on/container/file_to_cp.md /destination/on/host/{optional_new_name.md}`   

*Detach* from an interactive tty  
>on container:  
> `CTRL + P` then `CTRL + Q`

## run

## host clean up
Remove dangling images  
`docker rmi $(docker images --filter dangling=true -q 2>/dev/null) 2>/dev/null`

#### *Volume* option for run command  
Container destination must always be an absolute path.  
Host source may be an absolute path or named volume.  

#### User  


#### Ports  

Ports on containers must be specified at the time the container is RUN. There is not a way to open ports on the container after the fact.

###### sources  
* https://stackoverflow.com/questions/22049212/docker-copy-file-from-container-to-host#22050116
* https://stackoverflow.com/questions/17903705/is-it-possible-to-start-a-shell-session-in-a-running-container-without-ssh
