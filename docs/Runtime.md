# Runtime modification
In order to modify a map at runtime you'll have to add a paint generator to the blueprint layer you wish to modify.

1. Create a new `blueprint` layer  
2. Name it: `Island`  
3. Add a `paint` modifier to the layer  

You can now modify the layer by referencing the TileWorldCreator component and calling the ModifyMap method.
See following example:

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
  
## Build the map  
After modifying the map you need to execute the blueprint layer stack first, before executing the build layer stack to make sure all changes will be build.  
This can be done by using following code:

```csharp
// TileWorldCreator component reference
public TileWorldCreator twc;

// Subscribe to the OnGenerationComplete event so that we know when we can start building the map
void OnEnable()
{
    twc.OnBlueprintLayersComplete += BuildMap;
}


// This should be called after the map has been modified.
// After blueprint generation is complete the "BuildMap" method is being called
// Which rebuilds the tiles and objects
void ExecuteBlueprintLayers()
{
    // Execute blueprint layers after map has been modified.
    twc.ExecuteAllBlueprintLayers();
}


// Build the tiles and objects
void BuildMap(TileWorldCreator _twc)
{
    _twc.ExecuteAllBuildLayers();
}

```  
> Normally the tile and object instantiation layers will only rebuild the parts(clusters) of the mesh, which have been changed.


## Clear Map
To clear the paint layer at runtime simply use:  
 
    ```csharp
    // Clear map
    twc.FillMap("Island", false);
    ```  
    
## Fill Map
To fill a map use:  

    ```csharp
    // Fill map
    twc.FillMap("Island", true);
    ```  
    
## Copy Map
The copy map method works like the editor copy map functionality.
It copies the last output to the paint modifier.  

    ```csharp
    // Copy map
    twc.CopyMap(string _layerName);
    ```  

**Example**
Please also have a closer look at the `01_Runtime Editor` demo scene.  
This scene uses all the basic map modifications, and is a great start for creating your own runtime editor.
