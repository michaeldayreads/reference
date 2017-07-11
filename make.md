# Overview

`make` invokes `GNUmakefile`, `makefile` and `Makefile` - in that order - within the current directory and runs the default rule or goal, which is the _first_ rule in the file.

Current convention seems to favor `Makefile` since this more reliably shows as the top of a directory in many contexts.

In windows environments, a file extension may be required to ensure the OS knows what program to run to interpret the file, e.g. `makefile.NMK` for `NMAKE`.

Note that aside from the __default__ rule or goal, order does not matter.

`make <rule>` invokes the specified rule, usually referred to as the target.

`make <rule b> <rule a>` invokes rules in the order specified.

`make -C path/to/directory/` to target the  `Makefile` in another directory

`make -f path/to/file_not_named_Makefile` to target a file with a different name than the default filename.

> note: using a file extension of `.mk` will automatically trigger vim highlighting if syntax is on.

`make -n` print the commands that would be executed, but do not execute them.

A good practice is to have the first rule be a help target

`.PHONY: target_a target_b` a way to alert `make` not to associate targets with files of the same name.

To have errors on a shell command be ignored (i.e. avoid a non-zero exit code) prepend with a dash:

```
# makefile to remove temp files

.PHONY: tidy all

all:
     @printf "Available targets:\n"
     @printf "  tidy: remove all .tmp files"

tidy:
     -rm -r *.tmp
```

Recursively expanded variables are defined using `=`:

```
foo = $(bar)
bar = $(baz)
baz = All the things!

all:
     echo $(foo)

# prints "All the things!"
```

The value is stored verbatim and expanded at substitution.

vs.

Simply expanded variables, defined using `:=`:

```
foo := $(bar)
bar := $(baz)
```

Use `::` to indicate that there may be multiple targets of the same name that `make` should run:

```
baz::    ; @echo do foo
baz::    ; @echo do bar
```

> note the example did not really outline _why_ we would want to do this, though it might just be a simple way to separate step A from step B, rather than combine them into one recipe. One other possible application would be cases of using `include` to pull together functionality across makefiles that do different things but use the same targets.

## conditionals

# Concepts and Background

## explicit rule

## implicit rule

## variable definitions

## directives

The basic pattern is:

```
target: prerequisites
      recipe
```

A `target` is the name of a file or the name of an action to carry out.

A `prerequisite` is a file that is used as an input to the target.

A `recipe` is an action that `make` carries out.

# REFERENCE of rules, directives and built-in target names  

`.PHONY` Indicate to make that it should not look for a file, and thus a last updated time, of the name(s) that are specified as *phony* targets.

# options passed at invocation

## `-C` change directory

`-C <path/to/directory>` change to directory before doing anything further  

## `-d` and `--debug[=options]` debug



Sources
---
https://www.gnu.org/software/make/manual/html_node/index.html
Franken, Johannes. (2010). _Introduction to making Makefiles_ http://www.jfranken.de/homepages/johannes/vortraege/make.en.html
Free Software Foundation. (2016) _The GNU Make Manual_, version 0.74.
Graham-Cunmming, John. (2015). _The GNU Make Book_. No Starch Press.
Mecklenburg, Robert. (2004). _Managing Projects with GNU Make, 3rd Edition_. O'Reilly Media, Inc.
