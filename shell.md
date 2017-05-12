> Unless otherwise indicated, this document refers to bash shell.  

> Option lists on commands are non-exhaustive. The intention is to explain and highlight command line and scripting usage, not to clone the man pages.

# scripting

`#!/bin/bash` is a convention to let `execve` know what interpreter to load to execute a script. The actual path might vary, and can be determined with `which`.

## Variables

To set an environment variable:

`MY_VAR="value"`

The ALL_UPPERCASE is a convention. Lowercase can be used, but following the convention improves readability.

To clear the variable:

`unset MY_VAR`

### Variables and executable scripts

Scripts that have been made executable (`chmod +x foo.sh`) will run in a different process than the one where your invocation of that script takes place. This means that to ensure `BAR` is available to`foo.sh` we have to include the variable declaration in the invocation of the script: `BAR="baz" foo.sh`.

# builtins

`:`  From the documentation -- `Do nothing beyond expanding arguments and performing redirections. The return status is zero.`

Some use cases help:

* override a nonzero exit code

    ```
    if [ -f ${file} ]; then
        grep some_string ${file} >> otherfile || :
        grep other_string ${file} >> otherfile || :
    fi
    ```

* assign default values

    ```
    : ${FOO:=bar}
    ```

* infinite loops

    ```
    while :
    do
        <shell commands>
        <exit condition>
    done
    ```

* stub out a function

    ```
    function FleshMeOutLater {
        :
    }
    ```

Examples from [StackExchange][^1]

[^1]: https://unix.stackexchange.com/questions/31673/what-purpose-does-the-colon-builtin-serve

### 0_misc  

#### `$@` or all args

The example:

```
exec docker run --rm -it \
  -v $PWD:$PWD --workdir $PWD \
  ${DOCKER_PORT_ARGS} \
  -e "LOCAL_USER_ID=$(id -u)" \
  ${DOC_IMG} "$@"
```

This snippet is part of a shell script. A script can itself be called with multiple arguments following the script name.

In the context we see here, which is a script that puts us into a docker container anchored to the present working directory with network connections, we are able to include as arguments to our script additional options to invoke once the container is started. For example, we might invoke a `Makefile` recipe in some contexts and call yet another bash script in a different context. Using `"$@"` allows us to pass this later invocation as args in the invocation of the first script.   

`HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S: "`

other formatting options
```
cc      Century (either 19 or 20) prepended to the abbreviated year.
yy      Year in abbreviated form (e.g., 89 for 1989, 06 for 2006).
mm      Numeric month, a number from 1 to 12.
dd      Day, a number from 1 to 31.
HH      Hour, a number from 0 to 23.
MM      Minutes, a number from 0 to 59.
ss      Seconds, a number from 0 to 61 (59 plus a maximum of two leap seconds).
```

`ls -d */` list directories  

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

`ssh -F path/to/ssh_config_file host_name`

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

## `cd`

`cd -` Shorthand to change directory back to the last directory from which you changed directory. Thus:

```
$ pwd
> /foo/bar
$ cd ../baz
$ pwd
> /foo/baz
$ cd -
$ pwd
> /foo/bar
```

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

## compgen

`compgen -a` list all available aliases

## diff

`diff -i file_one.txt file_two.txt` output different lines, case insensitive

## find

`find ~/path/to/start/from -name pattern` where pattern is the name or partial name (* / ?) of the file

**note** Be sure to use quotes to prevent filename expansion, aka _globbing on the wild card `*`_

`find . -name '*py' ! -path '*test*'` Find all python files, but exclude directories that have "test" as part of their path, e.g. `/systest/` or `/test/`.

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

## printenv

List environment Variables

## rsync  
`rsync -a file_to_send.txt username@server:~/path/if/desired`  

## SCP

Secure copy

`user@host:path/to/file` format to specify target

`-r` recursive

`scp -F path/to/ssh_config_file path/to/file/to/copy.py host_name:/path/to/copy/file/into`

## sleep

`sleep <seconds>`  suspend execution for a minimum of seconds given.  

## source  

`source FILENAME [arguments]`  loads functions files  
For example, we may wish to `source ~/.profile`  re-load the profile after adding a new alias to our `.profile`.  

## tee

`ls -a | tee results.txt` both shows the output on stdout and also writes it to a file
`cat file_of_interest | tee -a results.txt` appends the file due to `-a` or `--append` flag

## test

Exits with a 0 (true) or 1 (false) based on the evaluation of an expression.

**NOTE** that since we are looking at a *return code* the logic can feel backwards! 0 == TRUE and 1 == FALSE because we want to be able to use the return code in the rest of a script!

`test` returns 1, since there is no expression

`[ ]`  this is an alias for `test`, and so returns exactly the same as above.

`[ "any string on its own evaluates to true."]` useful for debugging.

There are numerous flags that provide the ability to do focused testing or combine expressions in standard logic.

### options

`[ -d .git ]` returns 0 (true) in a directory under git source control.

`[ -f .git ]` would return 1 (false)

`[ -n "string" ]` tests if the length of a string is nonzero, would return 0 (true).

`[ -z "" ]` tests if the length of a string *is* zero, so would return 0 (true).

### useful patterns

`[ -n "$ENV_VAR_WE_NEED" ] || die "error message"`

## uptime  
`uptime` to see how long server has been running, users, load averages for 1,5 and 15 minutes  

## wc
`wc -l life_the_universe_and_everthing.sh` ideally this would return 42, as would running it :P   

### The real misc. debris...

### vagrant
`vagrant ssh -- -A -v`
