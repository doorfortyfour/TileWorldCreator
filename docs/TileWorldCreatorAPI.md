# API

```csharp
// Namespace
using TWC
```

### GetGeneratedBlueprintMap
  
  ```csharp
  WorldMap GetGeneratedBlueprintMap(string guid);
  ```  
  
  Returns the final generated map from a blueprint layer as a WorldMap class.  
  The WorldMap class contains the `worldPartitionTiles` dictionary which contains
  all generated data from the map.  
  
  `guid`  
  The layer unique guid or layer name as string
  
### GetMapOutputFromBlueprintLayer

```csharp
bool[,] GetMapOutputFromBlueprintLayer(string layerName)
```

Return the final generated map from a blueprint layer as a bool array.  

`layerName`  
The blueprint layer name







### GetMapOutputFromLayer

### GetTileData(string layername, Vector3 position)
Returns the tile data located at the position.

## Save & Load

### SaveLayerStack (string path)

### LoadLayerStackAndExecuteGeneration(string path)

### LoadLayerStack(string path)

## Execution

### ExecuteAllGenerationLayers

### ExecuteGenerationLayer(string layername)

### ExecuteAllInstantiationLayers

### UpdatePreviewTexture

### ModifyMap
### FillMap
### CopyMap

### GetAction(string layername, string guid)

### GetAction(string layername, int stackindex)

## Events

### OnGenerationComplete
### OnInstantiationComplete


# TileWorldCreatorWorldData

