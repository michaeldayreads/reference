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

#### strings

```
"one two three".split(" ").last => "three"
```


# The Ruby Programming Language
Flanagan && Matsumoto (2008)


In Ruby, everything is an expression.

## Structure && Execution

### Non code

`# comments`  

```
# multiline
# comments
```  

```
=begin
Embedded Documents
=end
```  

```
=begin rdoc
Embedded Document passed to ri Documentation api if it 
immediately precedes a Method, Class, or Module
=end
```

### Readability, both syntactic and conventional
- White space separates tokens
- `;` terminates a statement, though uncommon
- Any complete expression followed by a new line is evaluated
- a `\` at line end can be used to extend a complex statement to another line
- a `.` at line start, for long method chaining (1.9)
- `method(x + y)` == `method (x + y)` != `method x + y` (use -w)
- Ruby is __case sensistive__
- Punctuation is often syntactic, always expressive

```
$files			# global var
@data			# instance var
@@counter		# class var
Pi				# Constants are Capitalized

empty?			# Boolean-valued method / predicate
sort!			# In place, aka modify the object
timeout=		# Method invoked by assignment
```

### Keywords
```
__ENCODING__
__FILE__
__LINE__
begin
BEGIN
alias
and
break
case
class
def
defined?
do
else
elsif
end
END
ensure
false
for
if
in
module
next
nil
not
or
redo
rescue
retry
return
self
super
then
true
undef
unless
until
when
while
yield
```

### Kernal, Module, Class and Object class methods

#### keyword-esque
```
at_exit
attr
attr_accessor			# getter && setter
attr_reader				# getter
attr_writer				# setter
catch
include
lambda
load
loop
private
proc
protected
public
raise
require
throw
```

#### Common Global Functions
```
abort
Array
autoload
autoload?
binding
block_given?
callcc
caller
chomp
chomp!
chop
chop!
eval
exec
exit
exit!
fail
Float
fork
format
getc
gets
gsub
gsub!
iterator?
Integer
load
open
p
print
ptintf
putc
puts
rand
readline
readlines
scan
select
sleep
split
sprintf
srand
string
sub
sub!
syscall
system
test
trap
warn
```

#### Commonly used object methods
```
allocate
clone
display
dup
enum_for
equal?
extend
freeze
frozen?
hash
id
inherited
inspect
instance_of?
is_a?
kind_of?
method
methods
new
nil?
object_id
respond_to?
send
superclass
taint
tainted
to_a
to_enum
to_s
untaint
```

#### Identifiers
Identifiers are ultimately unique on the basis of bytes, not glyphs.

#### Syntactic Structure
_tokens_ combine to make  
_expressions_ which can be primitive, complex, or  
_statements_ which are technically expressions, though are distinct in that they control program flow.

_blocks_ are ordered sets of expressions associated with iterators using `{...}` or `do ... end`  

_bodies_ are control structures, methods, classes, modules and are denoted by key words specific to each type, covered in chapters 5,6, and 7.

#### File Structure
`#!/usr/bin/ruby -w` the -w is for warnings on ambiguous use of whitespace  
`# -*- coding: utf-8 -*-` encoding  
`require 'socket' ` networking library  
...  
script  
...  
`__END__`  mark end of code - data can follow and be accessed by IO

#### Program Encoding
Source Encoding - reading source, including strings in source

External Encoding - reading from files & streams

Internal Encoding - transcode external text as its read

#### Program Execution

The interpreter:  

- starts with `BEGIN` blocks
- goes line by line until:
	- a statement causes it to terminate
	- it reaches the end of the file
	- it reaches the logical end of the file at `__END__`
- before it quits, it looks for `END` statements and `at_exit` hooks  

## Data Types && Objects

### Numbers
Five built in classes, and three more in the standard library:

- Integer
	- Fixnum -- usually up to 31 bits
	- Bignum -- the rest
- Float -- includes real numbers as aproximations
- Complex
- BigDecimal -- arbitrary precision
- Rational

All are instances of `Numeric`.

__All numeric objects are immutable__.

For readability, underscores can be used for large integers to indicate thousands separators e.g. `1_000_000`

#### Other bases:

```
0b1111_1111		# binary 255
0377	 		# octal 255
0xFF			# Hex 255

```

#### Floating Point / Scientific

Numerals before and after `.`  

```
0.1.002e7		# scientific
```

#### Arithmetic
Be aware that base 10 decimals are approximations:
`0.4 - 0.3 == 0.1` evaluates to false on most implementations.
Use `BigDecimal` for financial.

> For scientific, no recommendation given even though acknowledged as difficulty.


### Text and Strings

#### Arbitrary Delimiters

```
%q(No need to escape ' or ")
%Q|same, but able to interpolate #{stuff}|
xml_test = %Q<<hot><name>#{name}</name><phone>#{num}</phone></hot>>
```

#### Here Docs

```
doc = <<HTML
<html><head><title>#{title}</title></head>
<body>
<h1>#{title}</h1>
#{body}
</body>
</html>
HTML
```

#### Backtick Shell Execution
```
`ls -al`	# sent to the kernal method
%x[ls -al]		# ditto
```
and it interpolates...

```
cmd = windows ? 'dir' : 'ls'
listing = `#{cmd}`
```

#### Mutability and efficiency
Strings are mutable, so  
`10.times {puts "test".object_id}`  
creates 10 objects, while   

```
test = "test"
10.times {puts test.object_id}
```
creates only one

`?x` denotes a character literal, in this case x. Post 1.9 its a string, earlier there are some quirks though its syntax only and not a class.

#### String Operators

```
a = "foo"
b = "bar"
a + b == "foobar"		# neither a nor b altered
a << b == "foobar" == a
"." * 3 == "..."

s = "hello"				# Examples are 1.9 - add .chr for 1.8
s[0]					# "h" 
s[s.length-1]	 		# "o"
s[-1]					# "o"
s[s.length]				# nil returned, but no error 
s[0] = "H"				# s now "Hello"
s[s.length-1] = "o!"	# s now "Hello!"
s[s.length] = "!"		# IndexError (!)
s[2,2]					# "ll" as a substring
s[s.length, 0] = "!"	# s now "Hello!" (!)
s[2..3]					# "ll" as a substring using range
s[-3..-1]				# "lo!" negative index using range
s[0...0] = "Say "		# "Say Hello!" insertion using range
s[8...10] = ""			# "Say Hell" deletion using range
```

_note_: Ranges use 2 indexes, string indexing uses 1 index and a length when two parameters.

#### Each

In 1.8, the method is simply `s.each` and in 1.9 we have:

```
s.each_byte
s.each_char
s.each_line
```

In 1.9 strings are sequences of strings length 1 and are not restricted to ASCII, and it can handle multibyte characters.

todo: return to this section post rvm

##### Interpolation

```
a = 0
"#{a=a+1}" * 3 	# returns "1 1 1"
```
Interpolation is only done once.

When sorting and comparing, recall Ruby is working with ASCII, so `"Z" < "a"`.

### Arrays
Mutable, untyped, and can be sparse. Negative indexes work. 

```
words = %w[x y z] 			# ["x","y","z"]
braces = %w% [ ] { } | % 	# ["[", "]", "{", "}", "|"]
```

### Ranges

### Symbols



## Expressions && Operators


## Statements and Control Structures
Conditionals  
The condition is an expression that is satisfied by evaluation to any value _other_ than `false` or `nil`.  

Many forms of expression:

```
if true
  p x
end

if true then
  p x
end

if true then p x end

if true;
  p x
end

if true; p x end
```
All valid.

`if` can also be a modifier  
`puts message if message # must all be on one line!`  

Be wary of precedence...  

_code_ if __expression__  

so, lets say `y = "foo"`. Then;

`y = x.invert if x.respond_to? :invert`  

means  

_y = x.invert_ if __x.respond_to? :invert__  

If x has an invert method, invert x and assign that value to y... if x __does not__ have an invert method, _nothing happens_ and y is still "foo".  

while  

`y = (x.invert if x.respond_to? :invert)`  

means

y = (_x.invert_ if __x.respond_to? :invert__)  

Which says create the object `y` and assign to it the result of the expression `x.invert if x.respond_to? :invert` which is `nil`.

`unless` is the opposite of `if`, can also be used as a modifier and can be used with `else` - though there is no direct equivalent to `elsif`.

`case` is an alternative to `if elsif ... else` 

```
name = case
```
