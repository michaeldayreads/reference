# General High Level

Docker Desktop does not give a clear warning that a "reset default settings" means it will wipe all the images on your unit.

# Dockerfile

A succession of command line instructions invoked by `build` to assemble an image.

# `exec`

Run a command in a background/daemon docker container.

`docker exec CONTAINER_ID ls`

or

`docker exec CONTAINER_NAME ls`

Also, you can use this to invoke a shell and inspect the container while other processes in it are working:

`docker exec -it CONTAINER_NAME bash`

# `run`

To run a container and attach to it via interactive terminal:

```
docker run -it -v `pwd`:/mount_path image:tag bash
```

To directly invoke a script or executable from your volume mounted pwd:

```
docker run -it -v `pwd`:`pwd` -w `pwd` image:tag sh path/to/script
``` 

To override the defined entrypoint (should be first argument):

```
docker run --entrypoint="/bin/sh" -it <image>:<tag>
```

To run a daemon:

```
docker run -d -v `pwd`:/mount_path image:tag tail -f /dev/null
```

To pass an environment variable to the container:

```
docker run -it --env TEST_DIR=$PWD -v `pwd`:`pwd` python:2.7 bash
```

To mount the pwd as the working directory:

```
docker run -it -v `pwd`:`pwd` -w `pwd` python:2.7 bash
```

^^^ refactored ^^^

# cli

## attach

`docker attach <name>`

Use `CTRL-p` then `CTRL-q` to detach and leave the container running.



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

`docker run CONTAINER_ID [OPTIONS]`

## host clean up
Remove dangling images
`docker rmi $(docker images --filter dangling=true -q 2>/dev/null) 2>/dev/null`

#### *Volume* option for run command
Container destination must always be an absolute path.
Host source may be an absolute path or named volume.

#### User


#### Ports

Ports on containers must be specified at the time the container is RUN. There is not a way to open ports on the container after the fact.

sources
* [Docker documentation](https://docs.docker.com/engine/reference/builder/)
* https://stackoverflow.com/questions/22049212/docker-copy-file-from-container-to-host#22050116
* https://stackoverflow.com/questions/17903705/is-it-possible-to-start-a-shell-session-in-a-running-container-without-ssh

docker run --rm -it -v $PWD:$PWD docker-registry.pdbld.f5net.com/velcro/attributions-generator:master /usr/local/bin/run-backends.sh $PWD

docker run --rm -it -v $PWD:$PWD docker-registry.pdbld.f5net.com/velcro/attributions-generator:master node /frontEnd/frontEnd.js $PWD
