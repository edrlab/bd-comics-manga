# bd-comics-manga

This EDRLab Working group is open to EDRLab members and a few Invited Experts.

## Goals

This work aims at creating a descriptive language representing next-gen BD / Comics / Manga, to be used as an "extension" or "module" (still to be defined) of the upcoming Web Publications / EPUB 4 standard.  

See also: [a post on the EDRLab website](https://www.edrlab.org/2017/07/07/bd-comics-manga-working-group-starting/) for the start of the WG.

Note: the [introduction to CBML](http://www.digitalhumanities.org/dhq/vol/6/1/000117/000117.html) referenced below shows shared motivations, although we are targeting new reading experiences, where CBML mostly targets analysis and study of existing works. The end result of our work is an authoring format, directly usable as an interchange format between ebook publishers and reading systems. 

## Initial choices

EDRLab advocates the use of a JSON manifest in Web Publications / EPUB 4; the different behaviors defined in the present work will threfore also be specified with a JSON serialization.

More precisely, EDRLab adocates the use of JSON-LD, a JSON representation of linked data, compatible with RDF. The WG will work on a JSON-LD expression of the language in a future step.

More details about the technical decisions taken during the course of the project are found in the section named [Technical decisions](./Technical decisions.md).

## Vocabulary, conceptual model

A BD, comics or manga contains a sequence of pages, often grouped in chapters. A traditional page contains a panel group, and panels contain speech balloons and captions. The boundaries between panels/balloons/captions can be ambiguous and they may overlap (e.g. a character in a panel with its arm in the adjacent panel; or a balloon going out of its source panel). Publications can be grouped in series and may belong to ebook collections.

We'll use therefore the following terms for publications:

* *visual narrative* (narration visuelle) (nom ombrelle) : the kind of publication we a studying; covers BD, comics,  graphic novels, mangas etc. A publication has a set of metadata and a reading order.
* *section*: a set of pages, which constitutes a reading unit. A chapter is a type of section. A section may have its own set of metadata, including a thumbnail (useful to ease the navigation in a strip).
* *page*: a "step" in the reading experience. Chosen because it relates to the notion of print "page" or Web "page". 
* *region*: a (usually square) region of interest that can be defined in a page around a *panel* (case), *balloon* (bulle), *caption* (légende) or any combination thereof.

Plus these terms for sets of publications:
* *series*: a set of publications belonging to the same narrative arc (usually ordered).
* *collection*: a set of publications grouped by its publisher (usually unordered)

Note: bib.schema.org defines Chapter rather thn "section".

### Navigation

In a "page navigation" reading mode, a user can move from page to page using a key, tap or swipe gesture. In a "region based navigation" reading mode, one can move from region to region using a key, tap or swipe gesture.

### Notes
Let's take Phalaina, or a visual narrative based on a set of interactive scenes: the notion of page is not so easy to define then. We'll assimilate the chapter or scene to a "page".

Extract from the CBML intro: <i>"The page is indeed one of the primary structural and compositional units of comics. In TEI the page is viewed as a "milestone," an empty marker within the flow of the text. In comics books (and similar documents), the page is not an arbitrary milestone, but a compositional feature — a composed container for "panels" and text."</i>


## Table of contents

The work is split in different sections :

* [Scroll](./Scroll.md)
* [Transitions](./Transitions.md) between pages
* [Transformations](./Transformations.md)
* [In-book update](./In-book update.md)
* [Parallax effects](./Parallax effects.md)
* [Multiple renditions](./Multiple renditions.md)

## References

* [IDPF Workshop on Sequential Art (Comics, Manga, Bandes dessinées, and new form), 2014, Paris, France](http://idpf.org/idpf-comics-manga-workshop-paris)

* [IDPF EPUB Region-Based Navigation 1.0](http://www.idpf.org/epub/renditions/region-nav/)

* [Readium Web Pub Manifest](https://github.com/readium/webpub-manifest/blob/master/README.md)

* [Web Animations (W3C)](https://www.w3.org/TR/web-animations-1/)

* [CBML](http://dcl.slis.indiana.edu/cbml/), the Comic Book Markup Language, and XML dialect based on TEI. Essentially add &lt;cbml:panel>, &lt;cbml:balloon> and &lt;cbml:caption>.

* [Schema.org VisualArtwork](http://schema.org/VisualArtwork), A work of art that is primarily visual in character.
