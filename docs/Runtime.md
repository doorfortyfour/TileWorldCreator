# Runtime modification
In order to modify a map at runtime you'll have to add a paint generator to the layer you wish to modify.

1. Create a new `blueprint` layer  
2. Name it: `Island`  
3. Add a `paint` modifier to the layer  

You can now modify the layer by calling:  

```csharp
// TileWorldCreator component reference
public TileWorldCreator twc;
// Modify map
// _x and _y are the map position
twc.ModifyMap("Island", int _x, int _y);
```
    
+ `_layerName`
  The blueprint layer name which has the paint modifier you want to modify
+ `_x`
  The x position on the map
+ `_y`
  The y position on the map
  
*Build the map*  
After modifying the map you need to execute the build layer stack to make sure all changes will be build.  
This can be done by using following code:

```csharp
ENTER CODE
```  


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
> It is strongly recommended to have a look at the 01_Runtime Editor demo scene.
