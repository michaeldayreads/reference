# running tests

`pytest test_file.py`  run all tests in this file.  

## `-k` or keyword flag
`pytest -k "test_foo" test_file.py`  runs tests with "test_foo" as part of name

## `--ignore=path/to/ignore`

## `-p no:cacheprovider`

Turns off the caching plugin. Can be useful when tests are running in a context where they do not have write capability (e.g. docker).
