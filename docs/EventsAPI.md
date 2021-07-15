# Events

## OnBlueprintLayersComplete
```csharp
OnBlueprintLayersComplete(TileWorldCreator tileWorldCreator);
```

Called after `ExecuteAllBlueprintLayers` or `ExecuteBlueprintLayer`  

**Example**  
```chsarp
  // Subscribe to event
  void OnEnable()
  {
    tileWorldCreator.OnBlueprintLayersComplete += BuildMap;
  }
  // Unsubscribe event
  void OnDisable()
  {
    tileWorldCreator.OnBlueprintLayersComplete -= BuildMap;
  }
  
  // Blueprint generation is complete we can now call ExecuteAllBuildLayers to build the map
  void BuildMap(TileWorldCreator tileWorldCreator)
  {
    // Build the map, do not force a complete rebuild
    tileWorldCreator.ExecuteAllBuildLayers(false);
  }
  
  
```


## OnBuildLayersComplete
```chsarp
OnBuildLayersComplete(TileWorldCreator tileWorldCreator);
```
Called after build layers stack is done. After `ExecuteAllBuildLayers`, `ExecuteBuildLayer`  

**Example**  
```csharp
 // Subscribe to event
  void OnEnable()
  {
    tileWorldCreator.OnBuildLayersComplete += Done;
  }
  // Unsubscribe event
  void OnDisable()
  {
    tileWorldCreator.OnBuildLayersComplete -= Done;
  }
  
  // Build map is complete
  void BuildMap(TileWorldCreator tileWorldCreator)
  {
    Debug.Log("Ready");
  }
```

