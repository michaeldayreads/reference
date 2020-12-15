# Effective Markdown

In addition to formatting cribs and usage examples, this document contains conventions used in markdown documents in this repo and within my username space on GitHub.

## Links, Sources and [foot|end]notes

It is easy to have links to webpages like [this one](https://pinboard.in/u:michaeldayreads).

```
[this one](https://pinboard.in/u:michaeldayreads)
```

It is also easy to refer to other documents in the same repo, for example we can refer to the [vim](vim.md) doc.

```
[vim](vim.md)
```

Similarly we can link to headers within the present document. This means we can call out other sections, such as [the top of our document](#Effective)

```
[the top of our document](#Effective)
```

And this can serve for light weight [foot|end]notes<sup>[1](#1)</sup>.

```
notes<sup>[1](#1)</sup>
```

## tables

### code

```markdown

| header 0 | header 1 |
|----------|----------|
| r0, c0 | r0, c1 |
| r1, c0 | r1, c1 |
| r2, c0 | r2, c1 |

```
### rendered

| header 0 | header 1 |
|----------|----------|
| r0, c0 | r0, c1 |
| r1, c0 | r1, c1 |
| r2, c0 | r2, c1 |


Footnotes
----

###### 1 

Perhaps not ideal, but it does work.
