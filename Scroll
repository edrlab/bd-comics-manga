# Scroll on variable pages

Historically, scroll can be vertical or horizontal. In Korea and France, most scrolls are vertical, but there are horizontal use cases also.

In some use cases, 
- the author wants to block the screen mode (landscape / portrait). 
- the starting point is not top-left but at some coordinates
- scroll is not "free" and the author wants to add "snap points". 

## Fragment in the page

A zone may be a panel ("case"), a set of panels or any other rectangular area of an image.

note: currently the W3C only defines rectangular media fragments. AHL also defines polygons and radial fragments: this may be complex to implement, therefore we stick with rectangles. 

note: the best practice is too use percentages.

issue = not all "cases" have the same size and the definition of the zoomed image can therefore be of low quality.

## Positioning

A fit may be applied on screen 'height', 'width', 'both', 'optimize' or 'custom'.

In EPUB FXL, the default "fit" is 'both'. We'll stick with it. 

'optimize' means that the fit is done on one dimension, which depends on the screen mode, in order to optimize the display of the image. 

'custom' allow to define a starting point and the minimum amount of date that must be displayed initially, via a rectangle defined inside the fragment.


## Snap points

They may be placed on each image, or placed on fragments of wide/long images. 

They will be used to:
- manage sounds
- manage layers (backgrounds)

study: study the CSS snap points.

## Should guided navigation and scroll be compatible in the same UX? 

see http://www.webtoons.com/en/action/brothers-bond/ep-2/viewer?title_no=1191&episode_no=3



