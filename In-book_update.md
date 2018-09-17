# In-book update

## Two different use cases

The first use case is the webtoon: The webtoon has a title, author, may have a cover and some descriptive metadata, but this is not a publication. It groups together individual stories, sold independently. Each story is therefore a publication, which may have its own ISBN. The overall webtoon acts as a series (and each story has a position in the series).

Note: [bib.schema.org](http://bib.schema.org/ComicIssue) defines "comic issue" in the first use case

The second case is a manga published chapter after chapter. The manga is sold as a whole, and when all chapters have been published, this evolutive narration will not be used anymore. The manga is the publication, and it gets an ISBN. This identifier is stable in time: it may even be created before the first chapter is released. individual chapters may have their own id, from a different scheme.

In the first case, the different stories will be archived independently. In the second case the complete manga will be archived. 

This is the second case which is of interest for us here.

## Sections and Metadata

Sections are released sequencially. 

The date of publication of the section is really useful there. It can be set in the future, indicating an upcoming section. 

A section with a future date of publication and no spine indicates that the chapter will be released at the given date; the reading app may notifiy the user when the date is reached.

A section with a future date of publication and a spine indicates that this is preview content.

## What's New
It is useful to indicate in the publication what has been modified in the book between two revisions.

The choice of the WG is the creation of a textual property named `whatsNew`. 

nb: a more complex list of items (a log) has also been discussed in the WG. 


