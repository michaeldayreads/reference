## metacharacters
`. ^ $ * + ? { } [ ] \ | ( )` 

`.`  any character except a null or new line  
`^`  beginning of the string  
`$`  end of the string  
`*`  zero or more as in `x*`  
`+`  one or more as in `x+`  

## character classes
`[]`  a character class to match `[abc]` or `[a-c]`  
`[()]`  character class of `(` and `)` as metacharacters are not active within classes  
`[^$]`  any character _except_ `$`  

### sequences that denote character classes  
`\d`  decimal `[0-9]`  
`\D`  non digit `[^0-9]`  
`\s`  whitespace `[ \t\n\r\f\v]` tab, new line, carriage return, form feed, vertical tab  
`\S`  non whitespace `[^ \t\n\r\f\v]`  
`\w`  alphanumeric `[a-zA-Z0-9_]`  
`\W`  non alphanumeric `[^a-zA-Z0-9_]`  

`[$\d.]` a character class sequence inside a character class matching numbers with decimals and dollar signs

## repetition
`x*` zero or more x and `x*?` !greedy  
`x+` one or more x and `x+?` !greedy  
`x?` zero or one x and `x??` !greedy  
`x{m,n}` x min of m times and max of n times and `x{m,n}?` !greedy  
