# Save and load
You can save and load a map at runtime using the methods:
Make sure to have a reference to the TileWorldCreator component in the scene.  
```csharp
    public TileWorldCreator twc;
    // Save
    _twc.SaveLayerStack(string _path);
    // Load
    _twc.LoadLayerStack(string _path);
    // Load and execute all layers
    _twc.LoadLayerStackAndExecuteGeneration(string _path);
```  
TileWorldCreator does not save the whole map array, it only saves the generation layer stack which makes the size of the save file
much smaller. By saving only the generation layer stack, it is also easy to re-generate the map by calling ExecuteAllLayers after loading is complete or simply use LoadLayerStackAndExecuteGeneration.

**Example**
> Please have a look at the runtime editor demo.
