# Multiple renditions

Exemples are:

* color + B&W
* finale version + blueprint (crayonné)
* multilingual

The manifest offers two complementary solutions :

## Links to alternate versions

A link is applicable when the different versions (term preferred here to rendition) are distributed as different publications, each with its own identifier. 

An example is the translation of a visual narrative in different languages, sold separately. In such a case, the relation between the current publication and the target publication may have multiple values, one being "alternate" (meaning that the target is an alternate publication) or, better, http://bib.schema.org/workTranslation (meaning that the target is a translation of the current publication), another being e.g. http://opds-spec.org/acquisition/buy (meaning that the way of acquisition of the target publication is buying it). The language of the target publication SHOULD then be indicated via an hreflang property. The e-distributor may even provide a price for the target publication, to be displayed by the user agent as a hint.  

```

{
  "rel": ["http://bib.schema.org/workTranslation", "http://opds-spec.org/acquisition/buy"]
  "href": "asterix10-ja.json",
  "type": "application/webpub+json",
  "hreflang": "ja",
  "properties": {"price": {"value": 12.99, "currency": "EUR"}}
}

```

## Alternate renditions

A sub-collection is applicable when all renditions of the work are published as a single publication, with a unique identifier (and price).

As example is a multi-lingual Manga. Alternate renditions each have their own set of metadata, spine and sections. The choice of a rendition among the set is made by the user agent, using the suitable combination of metadata, e.g. the "language" property.  

```

"renditions": [
  {
  "metadata": {
    "language": "fr"
  },
  "readingOrder":  [{},{}]
  },
  {
  "metadata": {
    "language": "ja"
  },
  "readingOrder":  [{},{}]
  }
]

```

## Rendition identifier

A rendition MAY also have an identifier, which is unique inside the visual narrative, and takes the form of a fragment identifier. A globally unique identifier for the rendition can be obtained by concatenation of the visual narrative URI and the rendition identifier, with a '#' separator.

## Renditions vs spin/sections

"renditions" replace "spine" and "sections" at the first level of the manifest

The JSON-LD @type for publications with multiple renditions is specific.

http://schema.org/Book for a standard publication.
http://to be invented for a book with multiple renditions.


TBC...
