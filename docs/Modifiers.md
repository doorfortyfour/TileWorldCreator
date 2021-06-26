# Modifiers

Modifiers are actions which modify a map.
TileWorldCreator comes with multiple ready to use modifiers but you can also implement your own.

## Add
Add the output of a layer to this layer

## Subtract
Subtract a layer from this layer

## Copy
Copy a layer in to this layer

## Expand
Expand the tile borders by one tile

## Shrink
Shrink the tile borders by one tile

## Invert
Invert the map

## Offset
Offset the map result by the offset amount

## PlayerPosition
The PlayerPosition modifier tries to find the best possible place 
to spawn a player. This is done by subdividing the map
in to 9 quadrants and searching for a fill tile in one of these quadrants. 
The output will be one single tile which can then be used by a object instantiation layer to instantiate the player object. 

`TopLeft`  
`TopCenter`  
`TopRight`  
`MiddleLeft`  
`MiddleCenter`  
`MiddleRight`  
`BottomLeft`  
`BottomCenter`  
`BottomRight`  

## Select
This is probably the most powerful modifier as it let's you select different parts of your map. 
> Combining multiple select modifiers can help extract very specific parts of your map. 

### Select by rules
You can add multiple rules for each selection type to filter the tiles you really want. 
Rules are defining how neighbouring tiles should be located for the selected tile. 
**Example**
Let's assume we only want to select the top tiles of a map. 


## Smooth
Smoothes the map by the smoothness amount. 
