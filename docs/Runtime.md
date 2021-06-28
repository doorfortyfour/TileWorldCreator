# Runtime modification
In order to modify a map at runtime you'll have to add a paint generator to the layer you wish to modify.

1. Create a new generation layer
2. Name it
3. Add a `paint` modifier to the layer

You can now modify the layer by calling:  

```csharp
// TileWorldCreator component reference
public TileWorldCreator twc;
// Modify map
twc.ModifyMap(string _layerName, int _x, int _y);
```
    
+ `_layerName`
  The generation layer name which has the paint modifier you want to modify
+ `_x`
  The x position on the map
+ `_y`
  The y position on the map
  
  
## Clear Map
To clear the paint layer at runtime simply use:  
 
    ```csharp
    // Clear map
    twc.FillMap(string _layerName, bool value=false);
    ```  
    
## Fill Map
To fill a map use:  

    ```csharp
    // Fill map
    twc.FillMap(string _layerName, bool value=true);
    ```  
    
## Copy Map
The copy map method works like the editor copy map functionality.
It copies the last output to the paint modifier.  

    ```csharp
    // Copy map
    twc.CopyMap(string _layerName);
    ```  

**Example**
> Please also have a look at the runtime editor demo scene.
