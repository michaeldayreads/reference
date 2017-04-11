# mu

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

A `prerequisite` is a file that is used as an input to the taget.

A `recipe` is an action that `make` carries out.

## flags  
`-C <path/to/directory>` change to directory before doing anything further  

Sources
---
Franken, Johannes. (2010). _Introduction to making Makefiles_ http://www.jfranken.de/homepages/johannes/vortraege/make.en.html
Free Software Foundation. (2016) _The GNU Make Manual_, version 0.74.
Graham-Cunmming, John. (2015). _The GNU Make Book_. No Starch Press.
Mecklenburg, Robert. (2004). _Managing Projects with GNU Make, 3rd Edition_. O'Reilly Media, Inc.
