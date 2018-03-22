# Multiple renditions

Exemples are:

* color + B&W
* finale version + blueprint (crayonné)
* multilingual

We have two solutions :

1/ a link

```
{
  "rel": ["alternate", "http://opds-spec.org/acquisition/buy"]
  "href": "japonais.json",
  "type": "application/webpub+json",
  "hreflang": "ja",
  "properties": ["price": {"value": 2.99, "currency": "EUR"}]
}
```

Note: here with OPDS properties added.

2/ a sub-collection at the publication level

```
"alternate": {
  "metadata": {
    "language": "ja"
  },
  "spine": "..."
}
```

TBC...
