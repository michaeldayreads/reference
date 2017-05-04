This document serves as a reference for markdown syntax aimed at a specific use case. I share that context here in the spirit of Creative Commons and in the event that like minded folks wish to collaborate on a refinement of markdown specialized along the themes stressed in this document.

Broadly, I write to learn. Markdown as a format for documents is fast to write, easy to read, and simple to search.

In addition to these basic qualities of markdown, the aim in this document is to have an alpha standard that provides human writable and readable methods to leverage machine readability, with goal of making the process of reading, researching and annotating more productive in the generation of rich data structures and high quality new documents.

Broad constraints:

* strong referencing to sources
* simple syntax based conventions for annotations
* parseable

# Fragments

The most general pattern is one of reading at different levels

Term

> `+ term`  
> Definition

Resolve internally

> `?`  
> Details

Resolve externally

> `!`  
>Details

Conflict

> `~`

Quote

> Simply use the expected format.

# Attributions and sources

A footnote style of source referencing can be used.

As an example, we'll recognize that a program is a particular kind of finite game as discussed by Carse.[^Carse_1986]

First, use the `[^title_of_work_1]` notation to get a simple superscript on your reference.

Then, at the bottom of the document, include

`[^title_of_work_1]:https://somelink.com`

For example, in creating this example a post from stackoverflow [^stackoverflow_15110479] was useful, and you can see it listed as the first source at the bottom of this document.

## naming conventions for those sources

In constructing the tag for the source, mimic the APA style of reference of author and year, e.g. Author(2017), thus `Author_2017`, `Author_2016a`, `Author_2016b`

For online collaborative sources, such as stackoverflow, reference the post id.

Sources

[^Carse_1986]: [Finite and Infinite Games](https://en.wikipedia.org/wiki/Finite_and_Infinite_Games)

[^stackoverflow_15110479]: http://stackoverflow.com/questions/15110479/markdown-and-footnotes-most-natural-format-missing
