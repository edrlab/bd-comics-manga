# Structure

## Distribution

A publication can be distributed either as a self-contained file (archive), or piecemeal over a network connection (streaming).

### Archive

The archive format is a zip file containing a mandatory `manifest.json` document at its root. All resources referenced in the manifest must be referenced relatively to the manifest file (thus contained in the archive).

### Streaming

The manifest can contain absolute or relative references to resources. **Do we allow references to resources on another server? (same-origin policy -- CORS?)**

All resources that are referenced using a relative URI must be referenced relatively to the manifest.

## In-book Update

Each update contains a main manifest (same manifest identifier) with additional sections.
New contents are identified by their timestamp in the section metadata.

### Archive

The reader application should merge the update with initial document:

- replace manifest
- add/replace resources
- cleanup?

### Streaming

The server provides a new manifest.

## Manifest

The main manifest name must be `manifest.json`. If the publication contains other manifests (alternate versions), they must be linked to the main manifest as `link` objects.

### Root

Each manifest contains the following elements at its root:

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
metadata   | **metadata** | publication metadata | Yes
links      | [**link**]      | an unordered list of relationships, as defined in [Readium Web Publication Manifest](https://github.com/readium/webpub-manifest). At least a `self` relationship is required. | Yes (main manifest)
spine      | [**page**]      | an ordered list of pages | No (\*)
guided     | [**fragment**]  | an ordered list of fragments, forming an alternate spine | No
sections   | [**section**]   | an ordered list of sections/chapters, typically used for chapter-based distribution | No (\*)
renditions | [**rendition**] | an unordered list of alternative renditions, identified by a `hreflang` property in their metadata | No (\*)
resources  | [**link**]      | an unordered list of files needed for rendition and not referenced in the `spine`, `sections` and `renditions` parts of the manifest | No

(\*) At least one of `spine`, `sections` and `renditions` is required.

### publication metadata

Based on [Readium Web Publication Manifest Metadata](https://github.com/readium/webpub-manifest#metadata). Additional elements:

Name       | Type        | Description           | Required
-----------|-------------|-----------------------|---------
changelog  | string      | Plain text change log | No

### link ###

Name       | Type        | Description           | Required
-----------|-------------|-----------------------|---------
rel        | string      | relationship to linked resource | No (except in "links" list)
type       | MIME type   | resource type         | Yes
href       | URI         | pointer to the resource, either as a file path inside the archive (relative to manifest), or as an absolute URL | Yes
hreflang   | string      | language of the resource (typical use: to specify an alternate manifest for a rendition in another language) | No
templated  | boolean     | true if `href` is a template | No (default = false)
properties | object      | properties attached to the resource; keys depend on the resource type and relationship | No

### rendition

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
metadata   | metadata    | rendition metadata | Yes
spine      | [**page**]      | an ordered list of pages | No (\*)
guided     | [**fragment**]  | an ordered list of fragments, forming an alternate spine | No
sections   | [**section**]   | an ordered list of sections/chapters | No (\*)

(\*) At least one of `spine` and `sections` is required.

### section

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
metadata   | metadata    | section metadata | Yes
spine      | [**page**]      | an ordered list of pages | Yes
guided     | [**fragment**]  | an ordered list of fragments, forming an alternate spine | No

### page/fragment

A page description can be either included in the manifest, or defined in another resource referenced in the manifest.

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
title      | string      | page title | No
type       | MIME type   | content type | Yes
href       | URI         | A fragment is defined by appending `#xywh=percent:x,x,x,x` to a page URI | Yes
properties | **properties** | page properties, as defined below | No
parallax   | **parallax** | parallax description | No

### page properties

Properties can be attached to any page, to define how the page is to be rendered (scrolling, etc), or to apply transitions to/from the page.

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
transition | **transition** | Transition effect between current page and next page | No
transition-forward | **transition** | Transition effect from this page to next page | No
transition-backward | **transition** | Transition effect from next page to this page | No
fit        | `fill`, `ratio#x:y`, `custom#...` | See [Scroll](./Scroll.md) | No
position-x | number      | See [Scroll](./Scroll.md) | No
position-y | number      | See [Scroll](./Scroll.md) | No
background | string      | background color in guided navigation | No

### transition

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
effect     | string      | effect name, e.g. `crossfade`, `push`, etc (as defined [here](./Transitions.md)) | No
duration   | number, or `slow`/`fast` | numeric value is in milliseconds | No
timing-function | string | function name (default = linear) | No
controllable | boolean   | transition is based on user movement (touch control) **should we separate "interactive" and "stoppable"?** | No
unique     | boolean     | transition should be played once during a reading session | No
resources  | [link]      | list of resources for transitions defined by a sequence of images | No

### parallax

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
layers     | [layer]     | List of layers, ordered from back to front. | Yes

### layer

Name       | Type        | Description | Required
-----------|-------------|-------------|---------
speed      | decimal number | 0 = fixed; 1 = finger speed when swiping | Yes
path       | SVG path | trajectory of the center of the layer | Yes
resources  | [resource] | sequence of images | Yes
opacity    | decimal number 0...1 | layer opacity (0 = transparent) | No
mask       | TBD | transparent areas, TBD | No

## Spine

A manifest must contain one or several `spine` objects. These `spine` objects can be found at these locations:

- at the root level,
- inside each section,
- at the root level of each rendition,
- inside each section of each rendition.

The reading engine is expected to display the document according to a dynamic spine generated by concatenating the relevant spines contained in the manifest, in this order:

- the root spine
- the spine in each section (in section order)
- the root spine of the active rendition
- the spine in each section of the active rendition (in section order)

The same logic applies to guided navigation, if `guided` elements are available.

## LCP

TBD (must be compatible with in-book update)

## Fallback mechanisms

