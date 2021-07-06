# Save and load
You can save and load a map at runtime using following code:
> Make sure to have a reference to the TileWorldCreator component in the scene.  
```csharp
    public TileWorldCreator twc;
    // Save
    twc.SaveLayerStack(string _path);
    // Load
    twc.LoadLayerStack(string _path);
    // Load and execute all layers
    twc.LoadLayerStackAndExecuteGeneration(string _path);
```  
TileWorldCreator does not save the whole map array, it only saves the blueprint layer stack as well as the map data like width and height, this makes the size of the save file
much smaller. By saving only the blueprint layer stack, it is also easy to re-generate the map by calling ExecuteAllLayers after loading is complete or simply use `LoadBlueprintStackAndExecute`.

## Build map
To build the map after loading, make sure to subscribe to the OnBlueprintLayersComplete event.

```csharp

public TileWorldCreator twc;

public void OnEnable()
{
    twc.OnBlueprintLayersComplete += BuildMap;
}

void BuildMap(TileWorldCreator _twc)
{
    _twc.ExecuteAllBuildLayers(false);
}

void LoadMap()
{
    var _path = Application.streamingAssetsPath + "/myMap.json";
    twc.LoadBlueprintStackAndExecute(_path);
}

```


**Example**
> Please have a look at the runtime editor demo as well.
