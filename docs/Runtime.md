# Runtime modification
In order to modify a map at runtime you'll have to add a paint generator to the layer you wish to modify.

1. Create a new generation layer
2. Name it
3. Add a `paint` modifier to the layer

You can now modify the layer by calling:
    
    // TileWorldCreator component reference
    public TileWorldCreator twc;
    // Modify map
    twc.ModifyMap(string _layerName, int _x, int _y);
    
+ `_layerName`
  The generation layer name which has the paint modifier you want to modify
+ `_x`
  The x position on the map
+ `_y`
  The y position on the map
