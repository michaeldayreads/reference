# digging about
`dir(obj)`  list of methods on object
`help(obj)`  A doc string list of methods on the object
`obj.__dict__` == `vars(obj)`  




# http server

`python -m SimpleHTTPServer 80`  python 2 simple server on port 80  
`python -m http.server 80` python 3 server on port 80  


# basics

`print str(1) + ". To concatenate numbers and strings use the str(n) method."`


# Data types  

## strings

`'answer all questions?'.translate(None, '?')`  --  rudimentary editorial implementation of translate  

## lists

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

# tricks, hacks, misc

`ternary_esque = a if (data != '') else b`  

Web server, one-liner
>`python -m http.server 80`

__Enumerate properties of an object__

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

# sources  

* [Python Documentation 2.7](https://docs.python.org/2/) and [3.5](https://docs.python.org/3.5/)
* [Python for Informatics - Severance (2013)](http://www.pythonlearn.com/html-270/index.html)
* [Think Python, 2nd Edition - Downey (2015)](http://www.greenteapress.com/thinkpython/)
* [pep-0257](https://www.python.org/dev/peps/pep-0257/)
