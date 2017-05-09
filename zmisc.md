This is a collection of miscellaneous small docs to keep the proliferation of files to a minimum.

# Atom editor

## keyboard shortcuts

`CTRL-G` goto a line number

# `nl`

Line numbering tool in Unix/Linux

`make | nl` will number the output of make

# pylint

The `ignore` flag has limited utility. A pattern to get around this is to write a shell script using find:

```
LIST="$(find . -name '*py' ! -path '*test*' ! -path '*docs*')"
for i in $LIST; do
    pylint $i -rn --notes=XXX,TODO,Todo,ToDo \
    --max-nested-blocks=6 \
done
```

## disable

Disable can be used at the command line as an option or with comments inline in the code.

The advantage to command line usage is in the use of a continuous integration invocation that applies the rules consistently to all files in the repo, rather than introduce an inline "local" disable, which is likely to simply fill the code base with exceptions.

You can disable by message name:

`pylint myfile.py --disable=fixme`

or by code:

`pylint myfile.py --disable=W0511`

or a whole "checker" or set of messages using the "verbatim" name of the checker.

`pylint myfile.py --disable=miscellaneous`

# safaribooksonline

`q` chapter
`f` increase font size
`g` decrease font size
`t` table of contents (toggle)

`u` top of page
`?` toggle keyboard shortcuts

# virtualenv

`virtualenv my_dir` where `my_dir` is a name of a directory where the new environment will live.

`source my_dir/bin/activate` to work within that virtualenv.

`deactivate` to exit it

## HipChat

`/code` to have chats code formatted

# svn  

**Check out an earlier revision than head**  
`svn co -r 2718 file:///var/svn/repo_or_file /target/path`

# Done

* Appointments and errands go on gcal/reminders
* Everything else on gitlab issues, kanban style

On gitlab:

* Tag as `md` or `f5`
* work out of that project
* Use due dates when there is one.
* Estimate, and then re-estimate as completed work is carved out or when the current estimate is exceeded.
* Milestones should represent the work completed during that time frame. 
