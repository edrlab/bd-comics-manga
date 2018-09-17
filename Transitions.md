# Transitions

Visual narratives are sequences of "pages",
and transitions appear when the reader moves from page to page.

A page may be the scan of a traditional comics page, or a single turbomedia image.

On touch devices, transitions are driven by the movement of the user's finger; the transition speed is driven by the movement speed.

Notel Apart from image-based transitions, the following effects can be implemented as [CSS 3 transitions](https://www.w3.org/TR/css-transitions-1/).

Transitions are set via the `transition` property applied to a page when the user navigates to the next page in reading order. `transition` represents a symmetrical transition: when a user navigates from a page to the previous page in reading order, the transition set on the target page is applied. 

## Transition types
`transition`is a json object and supports a `type` property. 
Here is a first list of useful types, most of them being well-knows in PowerPoint and the likes. 

### Crossfade 
The next page fades in as the current page fades out.

ex. `"type":"crossfade"`

### Slide (or Push)
The next page appears first on a corner, right (default), left, top or bottom, then pushes the current page to the other corner. The indication of a corner is given via a `from` property added to the transition.

ex: `"type":"slide","from":right"`

### Wipe
The next page appears first on a corner, right (default), left, top or bottom, then spreads to the other corner, as the current slide fades. The indication of a corner is given via a `from` property added to the transition.

ex: `"type":"wipe","from":"right"`

### Split
The next page appears first on the center (default), on a vertical or horizontal axis, then spreads to the corners, as the current slide fades.  The indication of a corner is given via a `from` property added to the transition.

ex: `"type":"split","from":"vertical"`

### Image based
A sequence of image resources are displayed between the current and next page. This type of transition is called `animated` and the set of images is expressed in an `images` property.

ex: `"type":"images","images":[]`

If a [timing function](#timing-function) property is provided, it will act on the duration of each individual image.

Note: alternatively, a duration per image could be set by the author, but in this case the discrepancy between the sum of (optional) image durations versus the global duration of the transition must be managed properly... Can or worms.

## Asymmetric transitions
The transition between two pages will usually be symmetrical, meaning that when moving from the current page to the next, then back, the reverse transition will be applied. 

Example: if the initial transition is a Slide from left, the reverse transition will be Slide from right. 

But the author may prefer to define a different effect for a forward and backward transition.

To allow such flexibility, a transition may be "forward" or "backward". Instead of a symmetrical transition, the author may then specify: 

* `transition-backward`: transition to be applied when moving back.
* `transition-forward`: transition to be applied when moving forward.
* when all 3 properties are defined, `transition` is ignored.

## Duration
For transitions triggered by e.g. a mouse click or image-based transitions, the effect may be scoped by a duration in milliseconds, or using the generic `slow` or `fast"` values. A `duration` property is therefore supported by a transition.

If the duration of the transition is not set, the user agent is free to select a default duration. It's also the user agent which will interpret the exact duration of the "slow" and "fast" values.

Note: the `slow` and `fast` values have been inspired by [jQuery Fading Methods](https://www.w3schools.com/jquery/jquery_fade.asp). Numeric values should be provided by the rendering engine, with guidance given in a "best practices" document.

## <a name="timing-function"></a>Timing function
A non-linear function may act on the duration of each frame of an image-based transition. A `timing-function` property is therefore supported by a transition. 

See [easings.net](http://easings.net) for a useful set of possible values.

## Controllable
The author may want the user to have a fine control on the transition, based on his movement (e.g. on a touch control), or prefer the transition to be un-stoppable when triggered. A `true/false` `controllable` property is therefore supported by a transition, the default value being `false`.

## Unique
The author may want the transition be played only once in a given reading session.
A boolean `unique` property allows to implement this behavior. The default value is `false`.

The definition of a "reading session" is up to the rendering application.



