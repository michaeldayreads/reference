trick n quirks  
`if __FILE__ == $0` checks to see if the current file is the name of the file used to start the program. Provides the means to include the file as a library.

`x**2` is exponentiation, x squared in this case  
```
=begin
this is a simple
haiku demonstrating a
multi-line comment
=end
```  
`"Lets see the #{variable} we are interested in"` string interpolation  

```
unless (hot && wicked_smart)
  puts "nice to meet you"
else
  puts "Pleasure. Care for a beverage?"
end
```

end methods with `!` to prevent the creation of a second object. Not clear if a namespace operation as it is in Python.

end methods with `?` to evaluate to a Boolean.  

for loops use `..` for inclusive ranges and `...` for exclusive

`for i in 1..10`

```
i = 1
loop do
  puts "doing thing #{i}\n"
  break if i > 2
end
```

can also be written

```
loop {
  puts "doing thing #{i}\n"
  break if i > 2
}
```

`next` keyword will proceed to the following value of the loop  

`each` is a method that iterates through objects.  

`3.times {print "there is more than one way to write a loop..."}  

naming conventions  
`local`  
`$global`  
`@instance`  
`@@class`  
`Constants`    

arrays  

`a = [2.71, 'mu', 0]`  

`a = %w{ 2.71 mu 0 } ` >> `["2.71", "mu", "0"]`  

hashes  
```
bibliography = {
  'Zen and the Brain' => 'James Austin',
  'Finite and Infinite Games' => 'James Carse',
  'Infinite Jest' => 'David Foster Wallace"
}
```

or  

```
timesRead = hash.new(0) # zero is the default value
timesRead['Infinite Jest']
>> 0
```

Control Structures  
`puts "make more coffee!" if oz < 2` is a _statement modifier_ version of `if` that is often more concise.  

Regex  
`/regex/`  
`line.sub(/water/, 'beer')` first beer  
`line.gsub(/water/, 'beer')` _all_ beer

Blocks  

A block is like an anonymous function or a lambda.

Blocks can handle setup, teardown and errors. 

---
BEGIN blocks and END blocks, inherited from perl, are a way to organize code [on stackoverflow](http://stackoverflow.com/questions/11620409/ruby-methods-at-bottom-of-script/11620522)  

Vertical Bars `||`  

"Vertical bars at the start of a code block are like parentheses in a method definition - they hold a list of parameter names. The `yield` statement is like a method invocation; it is followed by zero or more expressions whose values are assigned to the block parameters." (Flanagan, Matsumoto, 2008)

Iterators to Matz are any method that uses `yield`