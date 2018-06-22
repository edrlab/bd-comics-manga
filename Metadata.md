# Metadata

## Defined in the current draft of W3C Web Publications

- identifiers
- title (multilingual)
- date of publication
- date of last modification
- creators (authors)) with their role (localizable)
- progression direction (ltr/rtl -> a manga is rtl)
- privacy policy

### Remarks

EPUB 3 (and the current trend for Web Publications) stands that additional metadata will be described in e.g. ONIX. The issue is that Reading Systems don't process ONIX (or MARC or any specific) metadata.

## Defined in the Readium Web Pub Manifest (RWPM)

The RWPM metadata model is much more complete than the current W3C model. It is introduced in [Readium Web Pub Manifest Metadata](https://github.com/readium/webpub-manifest#metadata), and specified in details in [Readium Web Pub Manifest Default Context](https://github.com/readium/webpub-manifest/tree/master/contexts/default). In is based of schema.org properties and expressed as JSON-LD.

In short, we find here: 

- identifier
- title (multilingual)
- subtitle (multilingual)
- date of publication
- date of last modification
- contributors (author, translator, editor, illustrator, artist, colorist, inker, penciler, letterer, narrator plus a generic contributor)
- language(s)
- subject(s)
- numberOfPages
- duration
- publisher
- imprint
- description
- source
- belong_to
  - series
  - collection
- position
- progression direction

Details are found in the RWPM specification, which seems ready for classic visual narratives.

### Remarks

* http://bib.schema.org/ is a schema.org Bibliographic Extension, which contains proposals from Marvel and DC Comics plus from a W3C community group. Several RWPM metadata items are extracted from this standard vocabulary.
* The RWPM doesn't make use of the schema.org comics-series vocabulary, too much specific; the more generic series vocabulary is used instead. 
* Several WG participants would like to be able to express the original language of a translated work (ex. manga translated from japanese). Note that Electre models it as a metadata on the translator property.

### Several WG participants would like to ... 

* categorise the work, as in EPUB 3 (rendition vocabulary), as flow-paginated, flow-scrolled-doc, flow-scrolled-continuous ou flow-auto
* add metadata to individual panels (e.g. CBML).
* express the date of publiction of the next chapter in an evolving publication (in-book updates).
* allow the user to be notified of the publication of a new chapter.
* express metadata related to multiple renditions of a publication (e.g. color + B&amp;W)

## Sections

Question: will we make "sections" (array) an alternative to "spine" in the RWPM? i.e. does a publication contain "spine items" XOR "sections"? The WG seems to think it is the case.  

Solution 1: spine and sections are exclusive.
Cons: the object created out of the json structure is "polymorph". 

Solution2: spine and sections are both accepted in the same publication.
Pro: the object creation is simple. 
Cons: The reading order must be defined.
Proposal: the spine items are read before the sections. Therefore, a preface can be expressed as a spine item, before the chapter pages. But it means that pages like postface, at the end of the publication, must be embedded in one or several sections.   

## Metadata related to each section of a publication

The full set of metadata defined for publications may be applied also to each section. This is not a notion of override or inheritance (metadata for the section would be inferred from publication metadata, but metadata specifically defined in the section would replace or complement these). More simply, metadata defined at the level of the section describe the section, period. 

Note 1: there will be some exceptions, like publisher, belongs_to/series or collection.

Note 2: a section also supports a spine.

Sample:

```json
"sections": [
  {
    "metadata": {
      "@type": "http://bib.schema.org/Chapter",
      "identifier": "section3",
      "published": "2018-03-22T11:18:54+00:00",
      "title": "Chapitre 3 - Le retournement de situation",
      "position": 3
    },
    "spine": [{},{}]
  }
]
```

## Identifiers

A publication MUST have one identifier, as a URI. When applicable, it is an ISBN (e.g. urn:isbn:978031600000X). Alternatively, any scheme that enables the creation of globally unique identifiers (doi, ark etc.) is allowed as identifier. 

A section MAY also have an identifier, which is unique inside the visual narrative, and takes the form of a fragment identifier. A globally unique identifier for the section can be obtained by concatenation of the visual narrative URI and the section identifier, with a '#' separator.  

## Versioning

A visual narrative may be versioned. THe EPUB 3.1 sepcification defines the notion Release identifier for this purpose, which relies of the Unique Identifier and modification date. 

See http://www.idpf.org/epub/31/spec/epub-packages.html#sec-metadata-elem-identifiers-pid


## Date format
Date are formatted as W3C Date time (e.g. 2018-04-05T10:00:00+02:00).



