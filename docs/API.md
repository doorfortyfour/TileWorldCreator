# API

### GetGeneratedMap
  
  ```csharp
  public TileWorldCreator twc;
  TileWorldCreatorPartitioning generatedMap = twc.GetGeneratedMap(string guid);
  ```  
  
  Returns the final generated map from a layer as a TileWorldCreatorPartitioning class.  
  
### GetMapOutputFromLayer (string layername)
Return the final generated map from a layer as a bool array.

### GetMapOutputFromLayer (Guid guid)

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

