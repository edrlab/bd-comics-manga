# Panel navigation

Historically, scroll can be vertical or horizontal. In Korea and France, most scrolls are vertical, but there are horizontal use cases also.

In some use cases, 

- the author wants to block the screen mode (landscape / portrait). 
- the starting point is not top-left but at some coordinates
- scroll is not "free" and the author wants to add "snap points". 

## Fragmenting the page

A zone in a page may be a panel ("case" in French), a set of panels or any other rectangular area of an image.

note: currently the W3C only defines rectangular media fragments. AHL also defines polygons and radial fragments: this may be complex to implement, therefore we'll stick with rectangles. 

note: the best practice is to use percentages.

json sample:

	{
		"href": "page1.jpg#xywh=percent:5,5,15,15",
		"type": "image/jpeg"
	}

issue = panels can be of very different size and the definition of an image, once zoomed full screen, can therefore be of low quality.

## Positioning & Zooming

Let's consider a portrait viewport, a landscape viewport and an image fragment.

![](Scroll_elements.png)

A `fit` may be applied on the image `height`, `width`, `both`, `optimize` or `custom`.

### height

![](Scroll_fit_height.png)

### width

![](Scroll_fit_width.png)

### both

This corresponds to the notion of "aspect fit". In EPUB FXL, the default "fit" is `both`. We'll stick with it.  

![](Scroll_fit_both.png)

### optimize

his corresponds to the notion of "aspect fill". `optimize` (`fill`? `crop`?) means that the fit is done on one dimension, which depends on both the viewport and image aspect ratios, in order to optimize the display of the image.

![](Scroll_fit_optimize.png)

### custom

`custom` allows to define a starting point and the minimum amount of data that must be displayed initially, via a rectangle defined inside the fragment.

![](Scroll_fit_custom.png)

Sample: 

	{
		"href": "page1.jpg",
		"type": "image/jpeg",
		"properties": {
			"fit": "custom#xywh=percent:0,0,20,100"
		}
	}


## Snap points

They may be placed on each image, or placed on fragments of wide/long images. 

They will be used to:

- define a starting point (first snap point)
- define positions for previous/next events
- stop inertial scrolling on touch screens
- trigger actions (inline? through reference?)
	- manage sounds
	- manage layers (backgrounds)

study: study the CSS snap points.

	{
		"href": "page1.jpg#xywh=percent:5,5,15,15",
		"type": "image/jpeg",
		"properties": {
			"fit": "custom#xywh=percent:0,0,20,100",
			"snap-x": {"align": "left", "positions": [0]}
		}
	}

![](Scroll_snap_left.png)

## Fragement based Navigation

An ordered collection of fragments allows guided navigation between fragments.

Questions: 
should we allow multiple levels of navigation?
should this collection be separate, or should the fragments be included in the spine?
- if we have several collections, they must be separate.
should we accept several collections?
- interesting if they are conditions, media based 
- but requires metadata to select the good done.
response : no

## Transitions between fragments

The transisitons defined between pages are also applicable between fragments.


## Should guided navigation and scroll be compatible in the same UX? 

see [webtoons brothers-bond ep-2](http://www.webtoons.com/en/action/brothers-bond/ep-2/viewer?title_no=1191&episode_no=3)



