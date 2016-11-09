*Attach* to a running container with a shell tty  
>on host:  
>`docker exec -it <containerId> bash`  

*Copy* a file from a container to a host  
>on host:  
>`docker cp <containerId>:/path/on/container/file_to_cp.md /destination/on/host/{optional_new_name.md}`   

*Detach* from an interactive tty  
>on container:  
> `CTRL + P -> Q`

#### *Volume* option for run command  
Container destination must always be an absolute path.  
Host source may be an absolute path or named volume.  

#### User  


#### Ports  

Ports on containers must be specified at the time the container is RUN. There is not a way to open ports on the container after the fact.

###### sources  
* https://stackoverflow.com/questions/22049212/docker-copy-file-from-container-to-host#22050116
* https://stackoverflow.com/questions/17903705/is-it-possible-to-start-a-shell-session-in-a-running-container-without-ssh