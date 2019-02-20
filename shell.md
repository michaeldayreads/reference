> Unless otherwise indicated, this document refers to bash shell.  

> Option lists on commands are non-exhaustive. The intention is to explain and highlight command line and scripting usage, not to clone the man pages.

# commands

## `alias`

Map one token to many tokens, typically to save keystrokes on repetitive tasks.

It can be invoked per session, e.g. when you ssh to a host, and then `unalias` can remove it from the session if needed.

```
alias kc="kubectl"
# hack
# hack 
# hack
unalias kc
```

The more common pattern is to add aliases to `.bashrc` or `.bash_profile` so that they are built into each session.

## `apt`

> `apt-get update`
> resynchronize the package index files

`apt-get install foo`
> install foo

## `awk`

A useful way to combine results, e.g:

```
kubectl logs -n bar $(kubectl get po -n bar | grep foo | awk '{print $1}')
```

## brctl (bridge control - ethernet bridge admin)
`brctl show` list network bridges

## `bc`

Basic calculator.

Can be used interactively with `-i`, or can be passed a(some) file(s) which can contain more complex calculations, including functions.

[wikipedia](https://en.wikipedia.org/wiki/Bc_(programming_language)) provides reasonable examples.

## `cat`

Concatenate (combine) and print files.

Useful to quickly look at files with low risk of changing the file.

Useful to produce one file from two: `cat file_B >> file_A` produces 

```
file_A
file_B
```

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

## `chmod`

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
`g` file _group_  
`o` _other_ users not in the files group  
`a` _all_ users  

## compgen

`compgen -a` list all available aliases


## `curl`

Internet transfers for resources specified as URLs using Internet Protocols. 

`curl 10.1.2.3 -m 5`  specify a maximum of 5 seconds to complete the entire operation.

`-v` for verbose output

`-H` to specify a header

`--resolve <host:port:address>` method to prevent the use of the standard resolved address. Use in combination with a `-H 'Host: foo.com'` option to allow a router/switch/lb receiving the request to mimic owning the address in question.

For example:

```
curl --resolve foo.com:80:10.0.0.1 -H 'Host: foo.com' http://foo.com
```

### verifying output

use `curl -vs http://www.example.org/ > test.log 2>&1` to silently (no SDTOUT) redirect both the verbose output AND the response to a file to validate what the response was. This will include status code and headers.


## `date`

Manipulate and reference the date on the host.

Most common use is to output the date, as in:

```
date +%Y%m%d-%a-%H%m    # 20180108-Mon-1001
```

Keep in mind that the command is intended to alter the date of the system. Typically, one must sudo this command to have that impact, however, it is best to use `-j` to explicitly not use the output of whatever formatting or conversion you are doing as the new system time.

```
deadline=$(date -j -f "%Y-%m-%d" "2069-07-20" "+%s") # Apollo 11 centennial
```

This can be combined with `let` to perform calculations:

```
# how many days till a deadline?
dcd() {
    deadline=$(date -j -f "%Y-%m-%d" "2069-07-20" "+%s") # Apollo 11 centennial
    today=$(date +%s)
    let day_count_down="($deadline-$today)/(60*60*24)"
    echo $day_count_down
}
```

## `diff`

`diff -i file_one.txt file_two.txt` output different lines, case insensitive

## `env`

Used on its own to see environment (see [`printenv`](#printenv)) and additionally to override the environment within which a command will be executed.

## `exec`

Replaces the current process with a specific command. No subprocess is forked.

Can be a useful way to return to a new shell state.

## `export`

Setting a variable:

`FOO="bar"`

Establishes a key/value pair that is available to the current shell process without becoming part of the environment that is passed to a child process. This is commonly referred to as a _shell variable_, in contrast to an _environment variable_.

The `export` command exports a shell variable to the environment, making it available to child processes.

## `fc`

Fix Command builtin that edits and re-executes - or lists - a range of commands from the history.

> Be careful of the default behavior, which is to re-execute!

Suppose you perform `history | grep foo` and find the spot where you were working with `foo` and the result is:

`101 foo bar`

and you want to see what you did with `bar` before and after line 101.

`fc -l 98 103` will print those 5 lines, lets say they are:

```
98  cd foo
99  . bar arg-a
100 cat bar.log ../full.log
101 foo bar
102 rm bar.log
103 ls -la
```

and if you wanted to re-execute 99 to 102, but with `arg-b` you could

`fc -e vim 99 102`

and those commands would be copied to vim, you could modify the arg for `. bar` and then save and exit.

## `find`

`find ~/path/to/start/from -name pattern` where pattern is the name or partial name of the file (or directory).

**note** Be sure to use quotes to prevent filename expansion, aka _globbing on the wild card `*`_

`find . -name '*py' ! -path '*test*'` Find all python files, but exclude directories that have "test" as part of their path, e.g. `/systest/` or `/test/`.

## `gpg`  

`gpg --list-keys`  to get see what keys are on a system  
`gpg --export > all.gpg` to get all keys on key ring  
`gpg --import > all.gpg` to import that key set into another system  
`gpg -r {key_id} -e {file_name}` encrypt a file (adds .gpg to the end of the file name to name the new file)   


## `grep`

File pattern searcher.

Note that `egrep` is for extended regex (equivilent to `grep -E`) and `fgrep` is for literal characeters only and is equivalent to `grep -F`

`grep foo baz`  search baz for lines containing foo

`grep foo baz -v`  search baz for lines that do NOT contain foo

`grep foo baz -c`  returns match count

`grep foo baz --color` results colored for contrast

`grep -r foo .`             Search recursively from the current directory

`grep -r foo /baz`          Search recursively from the `baz` directory

`grep foo * -d skip`        Search ONLY the base directory: `-d` is the directory "action" flag; read, skip, recurse

A more complete example:

```
grep -rniI foo --exclude-dir=vendor --include \*.go .
```

This returns the `file:nn` where the line contains `foo`, but it does not search in the vendor directory and it only searches files that end in `.go`.

> Note: The format of `--flag=value` and `--flag value` are often equivalent. This example includes bothformats, but either can be used for the flags above.

### Options

`-e <pattern>` can be useful for special characters, such as `grep -rnI -e "-z" ./shell`


```
-n      line number
-h      no headers (i.e. filenames)
-i      case insensitive
-e      additional patterns, i.e. -e baz -e qux
-v      negative search (use -v -e foo -e bar to eliminate both)
-w      word matches only
-x      whole line
-l      files WITH match
-L      files NOT matching
-m      max count
-s      suppress errors for nonexistent/unreadable files
-q      quiet or --silent; exit immediately with 0 when a match is found
-I      ignore binary files
-C      context around; eg `grep -C 1 foo /baz`
-A      context after
-B      context before
```

Context

```
-A n    Print n lines after
-B n    Print n lines before
-C n    Print n lines before AND after

```

### Useful examples

Suppose you know a pattern occurs frequently across a number of files, and you simply want to see the variations of the patterns. 

```
grep -rh foo bar/ | sort | uniq
```

This returns a list of the examples. Note that the `-h` option omits the filename to ensure that the same example use in two files will not be seen as two `uniq` examples. A secondary `grep` with a more precise result could then be used to show context and/or list the files.

## `history`

`history | grep command-of-interest`  

```
270 blah-blah-blah  
271 command-of-interest  
272 blah-blah-blah
```

Then use the `!n` event designator to target the line you want to repeat...

`!271`

And use `!!` to reference the last command, as in `sudo !!` or:

```
find . -name foo
# presuming the result is/are the file/s you wish to edit...
vim $(!!)
```
see [`fc`](#fc)

### using search and replace

We can replace a specific string in a prior command easily:

```
!!:s/old/new   # run the last command but replace `old` with `new`
!42:s/old/new  # run history entry 42 but replace `old` with `new`
```

## `ifconfig` (WIP)

Configure a network interface.

`-a` Display details of all interfaces.

## `ln`

Create a hard or symbolic link. Most commonly it is the latter, as in:

`ln -s actual/directory/often/very/long/path short-hand-link`

## `ls`

Note on wildcards and globs: be aware that `.` - particularly at the start of a filename - can lead to some unintuitive ls results; e.g you are editing the file `stuff.txt` using vim, and vim has created a file `.stuff.txt.swp`, producing the following behavior:

```
> ls *swp
ls: *swp: No such file or directory
> ls .*swp
-rw-r--r--  1 foo  bar baz  2218 Nov  3 13:28 .stuff.txt.swp
```

```
-c # use time when last changed for sorting (-t) or long printing (-l)  
-C # column output
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


## `man`

Online manual pages. Note that for builtins use `help <builtin>` instead.

## `mtr`

Traceroute and ping. 


## `netstat`

Print network connections, routing tables, interfaces stats and more.

`netstat -rn -f inet

## `printenv`

List environment Variables

See:  
* [`env`](#env)
* [`set`](#set)


## `ps`

Process Status

most of the time what we are interested in is `ps aux` which gives us a more complete process list that we will in turn pipe to `grep`.


## `pushd` / `popd`

An alternative to `cd` that builds a stack of directories navigated that can later be retraced using `popd`.

Redirect output to `/dev/null` to invoke in a "silent" manner, e.g.;

```
pushd foo/bar > /dev/null
```

The option `-n` operates on the stack only, without navigating the user within the shell, thus;

```
pushd foo/bar     # add pwd, foo/bar to dirs stack AND cd to foo/bar
pushd -n foo/bar  # same as above, but do not change into that directory
```

The `-n` case might be useful to build a stack of dirs to act on later.


## `read`

Get input from the user. Also a useful way to wait for a keystroke to continue a script, e.g:

```
read -p "Press enter to continue"
```

More examples:

`read A && echo $A`  

`read -p "A proper prompt > " A && echo $A`

```
while read A; do
  echo $A
done
```

## `rsync`  
`rsync -a file_to_send.txt username@server:~/path/if/desired`  

## `scp`

Secure copy

basic format is `scp [options] source target`

`user@host:path/to/file` format to specify a remote source or target

### Common Options

`-r` recursive 
`-F` config file
`-i` identity file

`scp -r -F path/to/config_file path/to/copy user@host:relative/path/for/copies`

`scp -F path/to/ssh_config_file path/to/file/to/copy.py host_name:/path/to/copy/file/into`

Depending on how your ssh_config_file is set up, you may be using a `user@host_name:` format, in which case either specify a full path:

`/home/ubuntu/path/to/copy/file/to.txt`

or, alternatively just the partial path from the home directory for the user:

`path/to/copy/file/to.txt`

Note in the later case we presume the presence of the home path.

## `sed`

Stream editor. Takes files or standard input, modifies according to arguments, sends to standard out.

`sed '100,200!d' targetfile`  prints out lines 100 to 200. Pipe to `grep`...

`sed '100,200!d' targetfile | grep def` would be an easy way to see all the functions defined in a python file between those lines. Very useful if those lines are a very large class.

`env | sed '/<redact>/d'` to redact lines matching that pattern.

## `set`

List all variables and functions for the session.

Use `(set -o posix; set)` to exclude functions.

Use `set | grep foo` and `printenv | grep foo` to get evidence if `foo` is an environment variable or shell variable.

The most common pattern is to use `set` in a script to set the options for that script. Thus, including `set -x` in the top of a script elicits the same behavior as invoking the script with that option passed.

### options

See http://www.tldp.org/LDP/abs/html/options.html#OPTIONSREF

Those commonly referenced:

- `-e` exit on error
- `-x` print and expand each command


## `sed`

`sed` is a stream editor. The most common usage pattern is to perform substitutions on pipes or "in place" on existing files by use of the `-i` flag.

For instance, to replace `<MY_IP>` within a config file with the environment variable `my_ip` your bash script could include:

```
sed -i 's/<MY_IP>/'$my_ip'/' /path/to/config.file
```

Note the use of single quotes to allow interpolation and the `-i` in place flag.


## sleep

`sleep <seconds>`  suspend execution for a minimum of seconds given.  

## source  

`source FILENAME [arguments]`  loads functions files  
For example, we may wish to `source ~/.profile`  re-load the profile after adding a new alias to our `.profile`.  

## tar

To create an archive of the `foo/` directory within the current path:
`tar zv --create --file=foo.tgz foo`

The `z` option indicates zip, the `v` option tells tar to be verbose.

As suggested by `zv` the first token is a set of options that need not be preceeded by `-`, so:  
`tar czvf foo.tgz foo`
is a more concise and more common form.

Once created, you can examine the contents using:  
`tar --list --file=foo.tgz` OR `tar -tf foo.tgz`

To extract:  
`tar --extract --file=foo.tgz` OR `tar xf foo.tgz`

Be mindful of how the files you are archiving are being passed. If you include a path, that whole base path will be included in the tar, and present when you extract.

To change into the correct directory to be able to avoid extra prefixing file path elements, use:  
`tar czv --directory=/bar/qux --file=foo.tgz foo` or `tar czvCf /bar/qux foo`

> Note: `tar` expects the file paths to be absolute and will return an error when given a relative path.  

If we imagine our home directory is bar, and attempt to invoke:  
`tar czc --directory=/bar/qux --file=~/foo.tgz`  

We would get an error of:  
`tar: Failed to open '~/foo.tgz'`

Rather we should use:  
`tar czc --directory=/bar/qux --file=/bar/foo.tgz`

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

`if [ "$FOO" == "" -o "$BAR" == "" ]; then echo "do something if either one is missing"; fi` OR  

`if [ "$FOO" != "" -a "$BAR" != "" ]; then echo "do something only if both are present"; fi`  AND  

### options

`[ -d .git ]` returns 0 (true) in a directory under git source control.

`[ -f .git ]` would return 1 (false)

`[ -n "string" ]` tests if the length of a string is nonzero, would return 0 (true).

`[ -z "" ]` tests if the length of a string *is* zero, so would return 0 (true).

### useful patterns

`[ -n "$ENV_VAR_WE_NEED" ] || die "error message"`

## `uname`

Print basic system information. Use `uname -a` to get all information, or `man uname` to find option to target.

## uptime  
`uptime` to see how long server has been running, users, load averages for 1,5 and 15 minutes  

## visudo

Safely edit the sudoers file.

Can be a useful way to change the path for sudo, but be careful, as this essentially scopes the trusted binaries.

## watch

Display and refresh the output of another shell command.

`watch -n 0.1 -d foo` run the `foo` command every 0.1 seconds, refreshing the display and highlighting the differences.

## wc

`wc -l life_the_universe_and_everthing.sh` ideally this would return 42, as would running it :P   

## `xargs`

Construct an arguments list and execute the results.

Replace `bar` with `baz` in all files named `foo`

    find . -name foo | xargs sed -i '' -e 's/bar/baz/'

Find lines with `bar` in files named `foo`.

    find . -name foo | xargs grep --color bar

# SCRIPTS

`#!/bin/bash` is a convention to let `execve` know what interpreter to load to execute a script. The actual path might vary, and can be determined with `which`.

## Control Flow aka Logic & Conditionals

### `if`

```
if foo; then
  bar;
elif baz; then
  qux;
else xux
```

## Variables

To set an environment variable:

`MY_VAR="value"`

The ALL_UPPERCASE is a convention. Lowercase can be used, but following the convention improves readability.

To clear the variable:

`unset MY_VAR`

To clear a function:

`unset -f MY_FUNC`

### Variables and executable scripts

Scripts that have been made executable (`chmod +x foo.sh`) will run in a different process than the one where your invocation of that script takes place. This means that to ensure `BAR` is available to`foo.sh` we have to include the variable declaration in the invocation of the script: `BAR="baz" foo.sh`.

# builtins

`:`  The colon character is a null command, or a no op. From the documentation -- `Do nothing beyond expanding arguments and performing redirections. The return status is zero.`

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

See `tee` for method to have std out and also redirect to a file.

#### sftp  

`get filename.txt` transfers the file to the directory you logged into the sftp server from  

#### SPF  

Sender Policy Framework.  TXT records published on DNS that list hosts considered legit.  
`nslookup -type=txt domain.com`.  

#### `ssh`  

`eval "$(ssh-agent -s)"` Start an agent if one is not running.

`ls -al ~/.ssh` List present keys in most common path location (if any).

`ssh-add -l` List keys the agent has.

`ssh-add path/to/key` to add a key. Use `-K` if you wish to have the key added to a Mac keychain. 

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

### The real misc. debris...

#### yaml "scripts"

Continuous Integration/Delivery/Deployment tools often use `.yaml` files, with a portion of them being used for scripts. The intention is generally to have simple one line commands and to invoke shell scripts for more complex logic. In cases of simple logic, a structure such as:

```
- |
  if ["$FOO" == "bar"]; then
      echo "this would be an actual command or script..."
    else
      echo "and this would be the alternate case..."
  fi
- echo "and then back to regular commands"
```

### vagrant
`vagrant ssh -- -A -v`
