# Panel navigation

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

Transitions defined between pages are also applicable between fragments.


## Should guided navigation and scroll be compatible in the same UX? 

see [webtoons brothers-bond ep-2](http://www.webtoons.com/en/action/brothers-bond/ep-2/viewer?title_no=1191&episode_no=3)
