# Custom tiles

When creating your own tiles for TileWorldCreator, you have to make sure that they meet the following requirements:  

+ You will need 4 tiles for a complete map (edge, exterior corner, interior corner, fill)  
+ They must be square in size x and z. The height doesn't matter. Best way would be to create your tiles with a size of 1 in x and z. Within TileWorldCreator you can scale the global map (cell) and the tiles later.  
+ The pivot must be centered  
+ If you want to create a "2D" map, you can also use the unity default quad object (GameObject -> 3D Object -> Quad). Then you only have to assign your textures to it.

![requirements](img/tilesrequirements.jpg)
