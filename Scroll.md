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

issue: panels can be of very different sizes and the definition of an image, once zoomed full screen, can therefore be of low quality.

## Scaling

Let's consider a portrait viewport, a landscape viewport and two images or fragments: an image with a 1:1 aspect ratio and a wide image (5:1 aspect ratio).

![](scroll/portrait.png) ![](scroll/landscape.png) ![](scroll/square.png) ![](scroll/wide.png)
*Source: [https://publicdomainvectors.com](https://publicdomainvectors.com)*

A `fit` may be applied to the image so that it is scaled (up or down) to the viewport size. The aspect ratio must be preserved. Possible options are `height`, `width`, `both`, `optimize` and `ratio`.

### height

![](scroll/portrait_square_fill_left.png) ![](scroll/landscape_square_fit.png) ![](scroll/portrait_wide_fill_left.png) ![](scroll/landscape_wide_fill_left.png)

### width

![](scroll/portrait_square_fit.png) ![](scroll/landscape_square_fill.png) ![](scroll/portrait_wide_fit.png) ![](scroll/landscape_wide_fit.png)

### both

This corresponds to the notion of "aspect fit". In EPUB FXL, the default "fit" is `both`. We'll stick with it.  

![](scroll/portrait_square_fit.png) ![](scroll/landscape_square_fit.png) ![](scroll/portrait_wide_fit.png) ![](scroll/landscape_wide_fit.png)

### optimize

This corresponds to the notion of "aspect fill". `optimize` (`fill`? `crop`?) means that the fit is done on one dimension, which depends on both the viewport and image aspect ratios, in order to optimize the display of the image.

![](scroll/portrait_square_fill_left.png) ![](scroll/landscape_square_fill.png) ![](scroll/portrait_wide_fill_left.png) ![](scroll/landscape_wide_fill_left.png)

### ratio

`ratio` allows to define the minimum amount of image data that must be displayed, regardless of the relative aspect ratios of the image/fragment and the viewport. This option can be useful when the image is  very tall (resp. wide) with a landscape (resp. portrait) viewport.

Given an aspect ratio, the largest rectangle that fits inside the viewport is used to scale the image in "fill" mode.

- Example: 1:1 aspect ratio

![](scroll/portrait_wide_ratio1_left.png) ![](scroll/landscape_wide_fill_left.png)

	{
		"href": "page1.jpg",
		"type": "image/jpeg",
		"properties": {
			"fit": "ratio#1:1"
		}
	}

- Example: 4:3 aspect ratio

![](scroll/portrait_wide_ratio43_left.png) ![](scroll/landscape_wide_fill_left.png)

	{
		"href": "page1.jpg",
		"type": "image/jpeg",
		"properties": {
			"fit": "ratio#4:3"
		}
	}

- Example: 2:1 aspect ratio

![](scroll/portrait_wide_ratio21_left.png) ![](scroll/landscape_wide_ratio21_left.png)

	{
		"href": "page1.jpg",
		"type": "image/jpeg",
		"properties": {
			"fit": "ratio#2:1"
		}
	}


## Positioning

The scaled image may be positioned relative to the viewport by using `position-x` and `position-y` options.

The values given to these options are used as percentages relative to both the viewport and the image/fragment, so that the top left corner of the image/fragment is superposed to the top left corner of the viewport with (0, 0), and the bottom right corner of the image is superposed to the bottom right corner of the viewport with (100, 100). (50, 50) centers the image within the viewport.

- The default value for position-y is 50 (image centered vertically).
- The default value for position-x depends on the reading direction: 0 for left to right, 100 for right to left.

***Question: should the horizontal default always apply? When the image is narrower than the viewport, we may prefer it centered by default instead of moved to the left or to the right.***

- Example: center horizontally

![](scroll/portrait_square_fill_center.png) ![](scroll/landscape_square_fill.png) ![](scroll/portrait_wide_fill_center.png) ![](scroll/landscape_wide_fill_center.png)

	{
		"href": "page1.jpg",
		"type": "image/jpeg",
		"properties": {
			"fit": "fill",
			"position-x": 50
		}
	}

## Snap points *à sortir --> parallaxe*

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

## Fragment-based Navigation

An ordered collection of fragments allows guided navigation between fragments.

Questions: 
should we allow multiple levels of navigation?
should this collection be separate, or should the fragments be included in the spine?
- if we have several collections, they must be separate.
should we accept several collections?
- interesting if they are conditions, media based 
- but requires metadata to select the good done.
response : no

In guided navigation mode, background color information may be ignored.


## Transitions between fragments

The transitions defined between pages are also applicable between fragments.


## Should guided navigation and scroll be compatible in the same UX? 

see [webtoons brothers-bond ep-2](http://www.webtoons.com/en/action/brothers-bond/ep-2/viewer?title_no=1191&episode_no=3)

