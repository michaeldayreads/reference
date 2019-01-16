vim
---

# Formating and Syntax

## Indenting

`:set autoindent`

## Word wrap

`:set wrap | set linebreak`

# Spell Check

`:set spelllang=en`
`:setlocal spell`
`:set spellfile=/path/to/personal_spell_file/en.utf-8.add`

`]s` and `[s` to navigate.
`zg` to add a word to personal file.

# Invoking the shell within vim

`:! mkdir foo` will attempt to execute `mkdir foo` from the directory you were in when you invoked vim.


# text manipulation

## copy  
`yy` or `Y` will yank (copy) the current line  

`p` will paste it. If you are not in `INSERT` mode, vim will insert th

## delete
`x` current character to left  
`X` current character to right  
`dw` current word
`d$` cursor to end of line
`d^` cursor to beginning of line 
`dd` current line
`2dd` this and the next line
`dgg` this line and ALL above
`dG` this line and ALL below 

Note that `d` also copies the content, and `p` then puts or pastes it.  

## pasting from other applications

Vim is not always certain how to work with the system clipboard. Before pasting content from a non-terminal input:

`set: paste` lets vim know to not additionally format the incoming text.

`set: nopaste` returns behavior to standard.

# search

In standard mode, `/` starts a search string. You can make it case insensitive with `/\c`.

## characters

`fq` find next q (use `n` to move to next find)  
`%5` to look for braces, brackets etc.  

### replace single character under cursor
`r` then `x` would replace the character under the cursor with "x" without having to enter and navigate `INSERT` mode.

## and replace

### substitute aka _find and replace_  

#### without confirmation  

`:%s/ignorance/understanding/g` find and replace in __all lines__  
`:s/ignorance/understanding/g` find and replace in __current line only__  

#### _with_ confirmation  

`:%s/ignorance/understanding/gc` find and replace in __all lines__  
`:s/ignorance/understanding/gc` find and replace in __current line only__  

# folding

To set folding use `:setlocal foldmethod=<type>` where type can be:

- manual
- indent
- syntax
- expr
- marker
- diff

`foldmethod` may be abbreviated as `fdm` as in:

`:setlocal fdm=indent`

## Opening and closing

`za`    Toggle
`zo`    Open
`zc`    Close

## creating, modifying  
`zf3j` creates a fold from the cursor down three lines  
`zf/text` creates a fold from the cursor to the next instance of `text`  
`zd` delete the fold  
`zE` delete **all** folds  

## display & fold based navigation  

`zj` next fold  
`zk` previous fold  

`zR` decrease fold level to 0, aka open all  
`zr` decrease fold level by 1  
`zm` closes all open folds (increase fold level recursively)  

# navigation

## by character

` `|` `|` `
-----|-----|------
  |`k`|
`h`| | `l`
  |`j`|  

## by word  
`b` **first** character of _previous_ word  
`e` **last** character of _current_ word  
`w` **first** character of _next_ word  

combine with numbers...  

`3b` first character of 3rd word back  

`*` next occurrence of the word under the cursor  
`#` last occurrence of the word under the cursor  


## by line  

`0` or `^` will take you to the start of the line  
`$` will take you to the end  

`gg` first line of the file  
`G` last line of the file  

Goto a line by using the number followed by `G` or using `:` followed by the number. So...

`42` `G` is the same as `:42` `<enter>`  

## screen
`ctrl b` back one screen (beware tmux bindings)  
`ctrl f` forward one screen  
`ctrl d` forward 1/2  
`ctrl u` back 1/2  

## paragraph  
`ctrl }` next paragraph  
`ctrl {` last paragraph  

# inserting  

`30i-` then `<esc>` will insert a 30 hash line.  

`o` inserts a line below current line, and enters `INSERT` mode  
`O` inserts one *above* and enters `INSERT` mode  

# syntax highlighting and appearance  

`:syntax on` and `:syntax off` for file specific toggling  
`:set syntax=off` to have that setting persist for that file

Note that if the file extension has changed, the associated syntax may also change.

To ensure you get the syntax you want:

```
:set syntax=off
:set syntax=<language>
:set syntax=on
``` 

`:set cc=80`
`:highlight ColorColumn ctermbg=DarkGray` gives an offset bar at column specified above.

To determine what languages your vim is able to understand, the following commands within vim let us list those possibilities:

```
:echo glob($VIMRUNTIME . '/ftplugin/*.vim')
:echo glob($VIMRUNTIME . '/syntax/*.vim')
```

> Note that there are many, so a more targeted search - such as `/syntax/p*.vim'` when trying to remind yourself if python is spelled out (yep) or abbreviated will give us a shorter list to read.

> Troubleshooting: This is handy when file attributes are lost, such as during file recovery where your formatting is lost.

## python settings

```
set tabstop=8
set expandtab
set softtabstop=4
set shiftwidth=4
filetype indent on
```

# misc.

`.` repeats!  

## Time and Date stamp
`:r! date:x`


## line numbers  
`:set nu` to invoke -- `nu` short for `number`   
`:set nonu` to revoke  

## visual mode

key-binding     select mode
v               characters
V               whole lines
Ctrl-v          rectangular blocks

use `v` to enter visual mode, then use navigation keys to select text, which you may then `d` to cut or `y` to copy.  

This is a simple way to indent text:

    (navigate)  # to top of block to move over
    v           # enter visual mode
    j           # for each line to edit
    I           # to enter insert mode
    esc         # to complete the insert 

## undo

`u` undo last, aka backward in change history    
`<ctrl> r` redo last, aka forward in change history  

#### sources
http://vim.wikia.com  
http://alvinalexander.com/linux/  
http://vim.rtorr.com/  
https://www.linux.com/learn/  
http://www.openvim.com/  
