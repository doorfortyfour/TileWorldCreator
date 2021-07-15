# API

```csharp
// Namespace
using TWC
```

## GetGeneratedBlueprintMap
  
  ```csharp
  WorldMap GetGeneratedBlueprintMap(string guid);
  ```  
  
  Returns the final generated map from a blueprint layer as a WorldMap class.  
  The WorldMap class contains the `worldPartitionTiles` dictionary which contains
  all generated data from the map.  

  + `guid`  
  The layer unique guid or layer name as string


## GetMapOutputFromBlueprintLayer

```csharp
bool[,] GetMapOutputFromBlueprintLayer(string layerName)
bool[,] GetMapOutputFromBlueprintLayer(System.Guid guid)
```

Return the final generated map from a blueprint layer as a bool array.  

+ `layerName`  
The blueprint layer name  
+ `guid`  
The unique guid of the layer  

## GetTileData

```csharp
TileData GetTileData(string layer, Vector3 position)
```

Returns a tile data from the specified position  
  
+ `layerName`  
The blueprint layer name  

## SaveBlueprintStack

```csharp
SaveBlueprintStack(string filePath)
```

Save the complete blueprint layer stack  

+ `filePath`  
The file path including the file name and extension.  


## LoadBlueprintStack

```csharp
LoadBlueprintStack(string filePath)
```
Load the blueprint stack.

+ `filePath`  
The file path including the file name and extension.  

## LoadBlueprintStackAndExecute

```csharp
LoadBlueprintStackAndExecute(string filePath)
```
Load the blueprint layer stack and execute all blueprint layers.

+ `filePath`  
The file path including the file name and extension.  


## ExecuteAllBlueprintLayers
```csharp
ExecuteAllBlueprintLayers();
```
Executes all layers in the blueprint stack


## ExecuteBlueprintLayer
```csharp
ExecuteBlueprintLayer(string layerName);
```
Execute single blueprint layer specified by name.  

+ `layerName`  
The blueprint layer name  


## ExecuteBuildLayer
```csharp
ExecuteBuildLayer(string layerName, bool forceRebuild);
```

Execute specific build layer.  
 
+ `layerName`  
The build layer name  
+ `forceRebuild`  
Force a complete map rebuild or not.  


## ExecuteAllBuildLayers

```csharp
ExecuteAllBuildLayers(bool forceCompleteRebuild);
```

Execute all build layers from the build layer stack.  

+ `forceCompleteRebuild`  
Force a complete map rebuild or not.  

## UpdatePreviewTexture

```csharp
UpdatePreviewTexture(bool[,] map, Color color, Texture2D previousTexture)
```
Update the preview texture (thumbnail) based on the map and color.  
(Used by the paint modifier action)  

+ `map`  
The map which should be displayed as texture  
+ `color`  
The color of the preview texture  
+ `previousTexture`  
If not null, the last texture which should be merged with the new one.  


## ModifyMap
```csharp
ModifyMap(string layerName, int x, int y, bool value);
```

Modify the map at runtime. For this to work, a blueprint layer must have a paint generator assigned.  
 
+ `layerName`  
The blueprint layer name  
+ `x`  
The x position on the map  
+ `y`  
The y position on the map  
+ `value`  
The map modifier value. True = add tile, False = remove tile  

## FillMap
```csharp
FillMap(string layerName, bool value);
```

Fill paint map by the value (true or false)  

+ `layerName`  
The blueprint layer name with the paint generator  
+ `value`  
The value (true or false)  

## CopyMap
```csharp
CopyMap(string layerName);
```
Copies the last map output and adds it to the paint modifier so that it can be modified manually.

+ `layerName`  
The blueprint layer name with the paint generator  

## GetAction
```csharp
TWCBlueprintAction GetAction(string layerName, string guid);
TWCBlueprintAction GetAction(string layerName, int layerIndex);
```
Get an action from the blueprint layer stack by its guid or layer index

+ `layerName`  
The blueprint layer name  
+ `guid` or `layerIndex`  
The unique guid of the action or the layer index  

## SetCustomRandomSeed
```csharp
SetCustomRandomSeed(int seed);
```

Set a custom random seed for the map generation.  
When setting a custom random seed the random seed also gets activated. Use DisableCustomRandomSeed, to disable it again.

+ `seed`  
The custom random seed  


## DisableCustomRandomSeed
```csharp
DisableCustomRandomSeed();
```

Disable custom random seed
