# text manipulation

## copy  
`yy` or `Y` will yank (copy) the current line  

## delete
`x` current character  
`dw` current word  
`dd` current line  
`2dd` this and the next line  

## substitute aka _find and replace_  
### without confirmation  
`:%s/ignorance/understanding/g` find and replace in __all lines__  
`:s/ignorance/understanding/g` find and replace in __current line only__  
### _with_ confirmation  
`:%s/ignorance/understanding/gc` find and replace in __all lines__  
`:s/ignorance/understanding/gc` find and replace in __current line only__  

# folding
`zf3j` creates a fold from the cursor down three lines  
`zf/text` creates a fold from the cursor to the next instance of `text`  
`zd` delete the fold  
`zE` delete **all** folds

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

## screen
`ctrl b` back one screen (beware tmux bindings)  
`ctrl f` forward one screen  
`ctrl d` forward 1/2  
`ctrl u` back 1/2  

## paragraph  
`ctrl }` next paragraph  
`ctrl {` last paragraph  

## line  
`:42` takes you to line 42  


#### sources
http://vim.wikia.com  
http://alvinalexander.com/linux/  
http://vim.rtorr.com/  
https://www.linux.com/learn/
