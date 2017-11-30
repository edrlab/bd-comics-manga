# Transitions

Visual narratives are sequences of "pages",
and transitions appear when the reader moves from page to page.

A page may be the scan of a traditional comics page, or a single turbomedia image. 

On touch devices, transitions are driven by the movement of the user's finger; the transition speed is driven by the movement speed.  

## Effects
Here is a first list of useful transitions, most of them being implemented in PowerPoint and the likes. 

### Crossfade 
The next page fades in as the current page fades out.

### Slide (or Push)
The next page appears first on a corner, right, left, top or bottom, then pushes the current page to the other corner. 

### Wipe
The next page appears first on a corner, right, left, top or bottom, then spreads to the other corner, as the current slide fades. 

### Split
The next page appears first on the center, on a vertical or horizontal axis, then spreads to the corners, as the current slide fades.

### Images in-between pages
A sequence of image resources are displayed between the current and next page. 

A non-linear function may act on the duration of each individual image. A "timing-function" property is therefore supported by a transition. 

See [easings.net](http://easings.net) for a useful set of possible values.

Note: alternatively, a duration per image could be set by the author, but in this case the discrepency between the sum of (optional) image durations versus the global duration of the transition must be managed properly ... Can or worms.

## Progression
The transition between two pages will usually be symetrical, meaning that when moving from the current page to the next, then back, the reverse transition will be applied. 

Example: if the initial transition id a Slide from left, the reverse transition will be Slide from right. 

But the author may prefer to define a different effet for a forward and backward transition. 

To allow such flexibility, a transition may be "forward" or "backward". The author may then specify e.g. 

* "transition": symetrical transition.
* "transition-backward": there will be no forward transition, only a backward transition.
* "transition" and "transition-forward": "transition" will be used for backward transitions.

## Duration
For transitions triggered by e.g. a mouse click, the transition may be scoped by a duration in milli-seconds, or using the generic "slow" or "fast" values. A "duration" property is therefore supported by a transition.

If the duration of the transition is not set, the user agent is free to select a default duration. It's also the user agent which will interpret the exact duration of the "slow" and "fast" values.

Note: the "slow" and "fast" values have been inspired by [jQuery Fading Methods](https://www.w3schools.com/jquery/jquery_fade.asp).

## Controllable
The author may want the user to have a fine control on the transition, based on his movement (.e.g on a touch control), or prefer the transition to be un-stoppable when triggered. A `true/false` "controllable" property is therefore supported by a transition, the default value being `false`.


##  CSS transitions
Most transitions (but animations in-between pages) will be implemented as CSS 3 transitions (https://www.w3.org/TR/css-transitions-1/).



