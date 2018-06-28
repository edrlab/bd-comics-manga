# Parallax effects

## Use cases



##  Model

A page is made of N layers ("calques" or "couche" in French). 

Each layer has:
- a layer speed
- a linear path (v1) or complex trajectory (V2, Bezier curve) for the center of the layer
- an array of resources; e.g. sequence of images.

If the layer contains a PNG image or an HTML/CSS object:
- the layer has an opacity to make the content partially transparent 
- the image has transparent areas, 
through which one can see the layers below

Note: these notions of transparent areas and opacity are well known concepts in Photoshop. 

The layer speed values are decimal values. 
- 0 means that the layer is fixed
- 1 means that the layer moves at the speed of the finger during a swipe
  or at a system defined speed in the movement is triggered by a tap.  

## Fallback

Such a complex page SHOULD have a simple image or an HTML page as a fallback, for reading systems that can't process parallax efficiently.  

Alternatively, a JS lib may be attached to the document and - in a Web context - will render the parallax in a canvas.   

## Sound
