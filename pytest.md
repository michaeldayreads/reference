# running tests

`pytest test_file.py`  run all tests in this file.  

## `-k` or keyword flag
`pytest -k "test_foo" test_file.py`  runs tests with "test_foo" as part of name

## `--ignore=path/to/ignore`

## `-p no:cacheprovider`

Turns off the caching plugin. Can be useful when tests are running in a context where they do not have write capability (e.g. docker).

# Writing Tests

Before writing any new tests, familiarize yourself with the tests that have already been written and in particular with the types of `asserts` already used within the code base of interest.

`grep -rniI -C 3 assert /path` 

... shows assert statements and patterns already in use. 
