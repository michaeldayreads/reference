# cURL

A client for Uniform Resource Locators. To be precise, Uniform Resource Identifiers, though the RFC that formalized this distinction was in 2005, and cURL first shipped in 1998.

> Quick disclaimer: This document was produced in part because taking notes has proven an effective learning strategy. The emphasis is on usage important or interesting to the author of this document, and others may find the online [manpage](https://curl.haxx.se/docs/manpage.html) or the [everything curl](https://ec.haxx.se/) book - both of which are sources for this document - better references for their needs.

Though a common first use of cURL for a developer is to access an http or https resource, cURL supports many URL/URI schemes. The `://` sequence is what cURL uses to identify what the scheme is. Note that cURL also attempts to correct for one or three slashes, but two is what it in fact expects. In the case of `file://` we can use `file:///<path>` rather than `file://localhost/<path>` or `file://127.0.0.1/<path>`.

If the scheme is not provided, cURL attempts to deduce it from the hostname. When you are reading your shell history or a log, you will want to know what the scheme is; be explicit.

When using IPv6, use square brackets around the numerical address, e.g. `http://[::1/` for local host.

## Multiple URLs

cURL accepts multiple urls per invocation. If you use these feature, you can separate options for the URL using the `--next` option to specify a boundary:

```shell
curl --location http://example.com/1 --next
  --data sendthis http://example.com/2 --next
  --head http://example.com/3
```

## URL globbing

Use `[x-y]` for ranges - both numeric and alphabetic - and {0,1,...,n} for lists (arrays):

```shell
curl -O http://example.com/{web,mail}-log[0-6].txt
```

The globs can also be used in the output `-o` option for file naming, as in:

```shell
curl http://{site,host}.host[1-5].example.com -o "subdir/#1_#2"
```

Where the `#1` and `#2` will reference the `{site,host}` and `[1-5]` list and range respectively.

## config or option files

Option combinations used frequently can be combined into a file - with `# comments` - and passed to cURL invocations using `-K <path/to/file>`. More granular additional options can also be provided. Options in the file are read by line, and options that take arguments must have their arguments on the same line. Long options can omit the leading `--`, but otherwise the file is simply a list of command line options and optional comments.

The file also supports the use of `=` and `:` between the option and the argument to match some common "config" file expectations, but all three forms are equivalent to cURL.

A `.curlrc` file can be placed in the `HOME` or `CURL_HOME` to specify system wide options for all requests.

Note that this file option is an effective way to prevent command line leakage of passwords.

If the credentials you wish to use are in a `.netrc` file, use `--netrc-file <path/to/file>` or `--netrc` for the [default `.netrc` file](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html).


## HTTP & HTTPS

The HTTP verb is typically deduced from the options provided:
- `-d` or `-F` results in a POST.
- `-I` `--head` a HEAD.
- `-T` `--upload -file <path-to-file>` a PUT.


## basic use & examples

`curl 10.1.2.3 -m 5`  specify a maximum of 5 seconds to complete the entire operation.

`-v` for verbose output

`-H` to specify a header

`--resolve <host:port:address>` method to prevent the use of the standard resolved address. Use in combination with a `-H 'Host: foo.com'` option to allow a router/switch/lb receiving the request to mimic owning the address in question.

For example:

```
curl --resolve foo.com:80:10.0.0.1 -H 'Host: foo.com' http://foo.com
```

### verifying output

use `curl -vs http://www.example.org/ > test.log 2>&1` to silently (no SDTOUT) redirect both the verbose output AND the response to a file to validate what the response was. This will include status code and headers.

## Options

Can be placed anywhere in the line or read from [config](/#config-or-option-files) files.

Switch options, such as `--verbose` can be explicitly switched off using the `--no` prefix, as in `--no-verbose`.

To see all options, use `curl -h` from the command line. It is highly recommended to `| grep <search-term>` as there are 209 at this writing for cURL 7.54.0.

### Common

| Option | Description, Usage and Notes| Long Alias |
|--------|-----------------------------|------------|
| `-v` | Verbose output | `--verbose` |
| `-L` | Follow redirects | `--location` |
| `-A <string>` | User Agent | |
| `-d <string>` | Data, results in POST for http/s | `--data` |
| `-d @file` | Data file, results in POST for http/s | `--data` |
| `-F <content>` | Form content, results in POST for http/s | `--form` | 
| `-I` | HEAD for http/s | `--head` |
| `-T <file>` | Transfer file, PUT for http/s | `--upload-file` |

### Less common, but of interest

| Option | Description, Usage and Notes| Long Alias |
|--------|-----------------------------|------------|
| `-x <host>` | Proxy. Use HTTPS on the target host to set up an encrypted tunnel. | `--proxy <host>` |
| `-q` | Disable `.curlrc` | `--disable` | 


###### Sources

Most of the content of this document is an annotation of [everything curl](https://ec.haxx.se/) including many examples. When other sources are directly used, they are referenced inline in the document.