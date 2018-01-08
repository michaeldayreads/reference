# `as`

see:  
* [`try`](#try)  
* [`with`](#with)  

# `assert`

see [`try`](#try)

# `else`

see:  
* [`if`](#if)  
* [`try`](#try)

# egg

WIP

# `except`

see [`try`](#try)

# `finally`

see [`try`](#try)

# `flake8` -- shell

A commonly used installed package to identify variation from the PEP8 standards for code style.

`flake8 --show-source file.py`  includes snippets to clarify where in the source the issue has been flagged.

# `import`

## absolute

## relative 

# `map`

`data = map(str, raw_input()).split(' ')`   simple way to get "a b c" from stdin

```
# for a larger data set
n = int(raw_input())
queries = {}
for i in range(n):
    queries[i] = map(str, raw_input().split(' '))
```

# `pdb` - The Python Debugger

`import pdb; pdb.set_trace()`

Then use `s` to step through at low granularity, i.e. pdb stops when in can, though you may be at different levels of the stack.

Most often, the first pass is at `n` which is the next line in the function in the file where you placed the pdb.

Other commands:

?           List help
h <cmd>     Help on that pdb command
c           Continue:
s           Step:
a           Args: list the arguments of the current file.
p expr      Print: evaluate expression and print its value.
pp expr     Pprint: like print, but pretty print. 
w           Where: prints a stack trace.
d           Down: move the current frame one level down in the stack trace.
u           Up: move the current frame one level up in the stack trace.
q           Quit: The debugger is quit and the program is aborted.


# `pep8` -- shell

Style guide for python.

## Naming styles


`_single_leading_underscore` weak "internal use" indicator, will not be imported by `from my_module import *` but WILL be imported by `from my_module import _foo` ? 

# `raise`

see [`try`](#try)

# `try`

This section covers the various uses/patterns associated with `try`, including error handling.



## `as`

A means of designating a variable to which the exception object is assigned.

`except IndexError as my_index_error`  

The exception object is now available for further manipulation.

## `raise`



# `with`

# `virtualenv`

Tool to create distinct environments.

> __Warning__: Be mindful of 2 / 3 distinction. If you are on a unit that has both 2 and 3 installed, and then invoke `virtualenv new_ve` and `. /new_ve/bin/activate` you are in a python 2 ve, and the results of `which python` will return your ve, but the results of `which python3` will return the local install of python 3.

`virtualenv path/to/directory_for_ve_name`  python 2
`virtualenv -p python3 path/to/directory_for_ve_name` python 3

*^^ refactored*
----
*refactoring vv*


# dir -- and other useful methods of inspection/debugging.

`dir(obj)`  list of methods on object  
`help(obj)`  A doc string list of methods on the object  
`obj.__dict__` == `vars(obj)`  
`import keyword; keyword.iskeyword(sanity)` to see if "sanity" is a reserved keyword  
`keyword.kwlist` to see a full list  
`import __builtin__; dir(__builtin__)` to list python 2 builtins
`import builtins; dir(builtins)` for python 3 [^stackoverflow_22864221]
`locals()` Active local objects.
`globals()` Active global objects; contrast with `gc` below.

There is also the garbage collector (gc) interface, which can be used to look for memory leaks in addition to general introspection. The most common introspection command is:

```
import gc
foo = {'bar':'qux'}
gc.get_referents(foo)
```

To see all objects - of which there are thousands just to have python running:
`gc.get_objects()`

See `pdb`

# http server

`python -m SimpleHTTPServer 80`  python 2 simple server on port 80  
`python -m http.server 80` python 3 server on port 80  

# Data types  

## strings

`'answer all questions?'.translate(None, '?')`  --  rudimentary editorial implementation of translate  

suppose `uri = "10.1.2.3:80"`

`ip, port = uri.split(':')` returns two substrings of `ip` and `port`  

`ip = uri[:uri.find(':')]` returns one substring of `ip`

Note the latter is arguably _less_ pythonic, but none the less can be demanded by some linters when the second substring is not used later in the script.


### format

```
foo = "foo"
print("example 0: %s")
# example 0: foo
```

```
foo = 17
print("{0:d} {0:o} {0:X} {0:b}".format(foo))
# 17 21 11 10001
```

Types of substitutions:
b   binary
c   character
d   decimal
o   octal
x   hex (lowercase)
X   hex (uppercase)
n   number (using local settings for number separators)
''  None. Same as d.

Floating point:
e   Exponent
E   Exponent (uppercase)
f   Fixed
F   Fixed (uppercase)
g   General; f until too big, then e.
G   General (uppercase)
n   Same as g, but local.
%   Multiples by 100, f, and percent sign.
''  Same as g, but at least one digit after decimal.

```
def print_formatted(num):
    """Print a table of numbers 1 to num in decimal, oct, HEX, and binary."""

    width = len('{0:b}'.format(num))

    for i in range(1, num):
        for base in 'doXb':
            print '{0:{width}{base}}'.format(i, base=base, width=width),
        print

num = int(raw_input))
print_formatted(num)
```

##lists

Lists are mutable, unlike strings.

`examples = ['a',2.0,['b','c']]`  --  format  
`examples[1]` returns `'2.0'`  --  item by index  
`examples[-0]` returns `'a'`  --  item by negative index (right to left)  
`'a' in examples` returns `True` or `False`  --  Check if a list contains a value using _in_  
`examples.index('a')`  --  returns `0`  -- Find the _index_ of an item  
`examples.pop()`   --  returns `['b','c']`  **mutates list**  
`examples.pop(0)`   --  returns  `'a'`  **mutates list**  
`for example in examples: print example`  --   _traverses_ the list  
`for items in []` produces neither results nor errors
`['a','b'] + ['a','b']` returns `['a','b','a','b']`  --  concatenate lists  
`['a','b'] * 3` returns `['a','b','a','b','a','b']`  --  repeat lists  
`e2 = ['a', 'b', 'c', 'd', 'e', 'f']`  _using a longer example for slicing..._  
`e2[1:3]` returns `['b','c']`  --  slice is inclusive of _start_, but not _end_  
`e2[0:]` returns e2, and `e2[0]` returns `'a'`  
`e2[:6]` returns e2, yet `e2[6]` returns an _IndexError_  **interesting** result  
`e2[1:1] = ['alpha','beta']`  
makes e2 `['a', 'alpha', 'beta', 'b', 'c', 'd', 'e', 'f']`  -- **mutates list**  

`examples.append('d')` makes examples `['a',2.0,['b','c'], 'd']`  -- append **mutates list**  
`another = example` means `another is example` is `True` -- **interesting** namespace result  
`another = example[:]` creates a copy and `another is example` is `False`  -- copy lists  
`e3 = ['d','e']` third example  
`e2.extend(e3)`  
makes e2 `['a', 'b', 'c', 'd', 'e', 'f', 'd', 'e']` and e3 is _unmodified_   --  **interesting** result  

`e2.sort()` returns void, e2 is now `['a', 'b', 'c', 'd', 'd', 'e', 'e', 'f']`  -- **interesting** result  
`e2.remove('e')` returns void, and removes _last item added_ with that value  
makes e2 `['a', 'b', 'c', 'd', 'e', 'e', 'f']`  --  **interesting** result  

`scores = [99,88,72]` numerical example for built in functions  
`len(e3)`, `max(scores)`, `sum(scores)`, `min(e3)`  -- built in functions, `sum()` requires numerical values  

## Dictionaries

Dictionaries are key/value maps and are not ordered. To return a value, reference the key. Referencing a key that does not exists returns a KeyError, which can be easily avoided using `in`. To see if a value exists in a dictionary without knowing the key, produce a list of the values using `not_empty.values()` and then `in`. Note that `in` is a linear search for lists, and therefore expensive, whereas `in` for dictionaries uses a hash table. `get(_key_, _default_)` gives the ability to return the value associated with a key _or return a default_. Note that the method does not create a new key and set that default, it only returns the default if no key is found.

`mdd = dict()` or `mdd = {}` --  create an empty dictionary  
`mdd = {'mu':'emptiness preceding all things','computable':'recursively enumerable'}`  --  non empty
`mdd['key'] = 'algorithm connecting meaning and information'` -- add item  
`mu in mdd` returns Boolean, `True` in this case  --  use `in` to check for a key  
`definitions = mdd.values()` returns a list of values, against which `in` then works  -- find a value  
`mdd['magic'] = mdd.get('magic', 'abracadabra')`  --  used only for initialization  
`mdd[mu] = mdd.get(mu, 0) + 1`  --  use `get` method to set a new value to the default & iterate  
`mdd.get('unknown', 'No definition provided')`  --  used for graceful query failure  
`for terms in mdd: print terms, mdd[terms]`  --  list out the dictionary  

## Tuples
Immutable sequences that are hashable and comparable.

Tuples can be compared and lists of tuples can be sorted. Python looks for the first _difference_ between the tuples. This lends itself to Decorate Sort Undecorate; build a list of tuples with sort key(s), sort them, extract vales in another list. Since the sort keys have to come first, the tuples must be built in the right way.

`t = tuple()`  --  empty tuple
`t = ('a',)`  --  singleton tuple
`t = 'a', 1, ['b','c']`  --  syntactically correct  
`t = ('a', 1, ['b','c'])`  --  common notation for readability  
`t2 = tuple('mu')` points t2 to `('m','u')` `t3 = tuple(['m','u'])` points t3 to `('m','u')`  
`t2 == t3` returns `True` whereas `t2 is t3` returns false  --  **interesting**  
`t[1]` returns `1` and `type(t[1])` returns `int`  --  slice tuple for item type  
`t[1:2]` returns `(1,)` and `type(t[1:2])` returns `tuple`  --  slice tuple for tuple  
`t = t[:1] + ('b','c')` returns `('a','b','c')`  --  refer t to new tuple object  
`username, domain = email.split('@')`  --  use tuples to assign multiple variables  
`Last, First = First, Last`  --  tuple idiom to swap values  
`mdlist = mdd.items()`  --  returns list of tuples of key value pairs, now sortable by key first  
`for term, def in mdd.items: mddeflist.append((def, term))`  --  sortable by value first  

consider:

    terms = {  
      ('code', 'verb', 0): 'write code',  
      ('code', 'verb', 1): 'encrypt',  
      ('code', 'noun', 0): 'programming instructions'  
    }`

and...

`for word, category, use in terms: print word, category, use, terms[word, category, use]`  

which produces the very readable output of:

    code verb 0 write code  
    code verb 1 encrypt  
    code noun 0 programming instructions  

Or, we could `terms.sort()` and...

    for term in terms:
      entry, definition = term
      word, category, use = entry
      print word, category, use, definition

Readable output sorted by word, then semantic category, then commonality of use with definition provided:

    code noun 0 programming instructions
    code verb 0 write code
    code verb 1 encrypt

# Exceptions and exception handling

Patterns [^Lutz_2013]

## try/except

Use the next pattern instead...

> Explicit is better than implicit. [^zen_of_python]

## try/except/else

## try/finally

Still raise the exception, but clean up first.

In practice, it seems the `with` command is preferable. If needed, define your own class implementing the magic methods of `__enter__` and `__exit__`.

## try/except/else/finally

## nested try/except within try/finally


# working with packages

## Development mode

When working in/on a package it is often useful to invoke `python setup.py develop` to create an `egg-info` directory or an `egg-link` file that links to a project's code.

When you are done with a development task, use `python setup.py develop --uninstall`.

# tricks etc.

## ternary operator

Python lacks a ternary operator, however, the following can serve in some instances:

`ternary_esque = a if (data != '') else b`  

## Web server, one-liner
>`python -m http.server 80`

## Enumeration

```python
for name, value in inspect.getmembers(target_object)
    print(name)
```

## command line

__clear the screen__  
'Ctrl' + 'L' on unix  

`qc = os.system("clear")` wrapped in a lambda function (or windows equivalent) if 'Ctrl' + 'L' does not work

`vars()` to see what is in local memory when at the command line

# style, convention and readability

## doc strings
_pass_

# concepts

## Assignment
Associates a name to an object. It is a namespace operation. When Python sees `a = 1` it creates an integer object with the value 1 and assigns the name 'a' to it. When we declare `b = a` Python adds another reference to the object '1', but there is only one object.

sources  

[^Lutz_2013]: [Learning Python, 5th Edition](  https://www.safaribooksonline.com/library/view/learning-python-5th/9781449355722/)
[^Phillips_Romano_Hattem_2016]: Python: Journey from Novice to Expert.
[^zen_of_python]: https://www.python.org/dev/peps/pep-0020/
[^stackoverflow_22864221]: https://stackoverflow.com/questions/22864221/is-the-list-of-python-reserved-words-and-builtins-available-in-a-library

* [Python Documentation 2.7](https://docs.python.org/2/) and [3.5](https://docs.python.org/3.5/)
* [Python for Informatics - Severance (2013)](http://www.pythonlearn.com/html-270/index.html)
* [Think Python, 2nd Edition - Downey (2015)](http://www.greenteapress.com/thinkpython/)
* [pep-0257](https://www.python.org/dev/peps/pep-0257/)
# Pytest

## running tests

```
pytest                                      # use pwd as root dir, find tests
pytest -v                                   # verbose output
pytest path/to/test_file.py                 # run tests in test_file.py
pytest path/to/test_file.py::test_foo       # run only test foo in test_file.py

# some options

pytest -k foo               # run tests/classes matching foo
pytest -x                   # exit on first error / failure
pytest --lf                 # run only tests that failed last time
pytest --ff                 # run all tests, but failed ones first
pytest -l                   # show locals in traceback
pytest --collect-only       # collect but do not run
pytest --pdb                # start pdb on error
pytest -s                   # same as --capture=no i.e. stdout while testing
pytest --tb=long            # show full (available) traceback
pytest --durations=n        # show n slowest tests
pytest --durations=0        # show times for ALL tests
pytest --markers            # list markers
pytest --fixtures           # list fixtures
```

### `--ignore=path/to/ignore`

### `-p no:cacheprovider`

Turns off the caching plugin. Can be useful when tests are running in a context where they do not have write capability (e.g. docker).

_NOTE_: `pytest -h` lists help based on directory, as `conftest.py` files in the path can impact what options, markers, and fixtures are available.

## Writing Tests

Before writing any new tests, familiarize yourself with the tests that have already been written and in particular with the types of `asserts` already used within the code base of interest.

`grep -rniI -C 3 assert /path` 

... shows assert statements and patterns already in use. 
