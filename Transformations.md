# Transformations

## In-page transformation, before a transition
Use case: the user starts moving from a page to the next. A transformation is applied to the page; it may be tied to the movement of the user (touch use case); at the end of the transformation, the page to page transition is applied. 

### Images in-between pages
A sequence of image resources are displayed between the current and next page. 

If a [timing function](#timing-function) property is provided, it will act on the duration of each individual image.

Note: alternatively, a duration per image could be set by the author, but in this case the discrepancy between the sum of (optional) image durations versus the global duration of the transition must be managed properly... Can or worms.