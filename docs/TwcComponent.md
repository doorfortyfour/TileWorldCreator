## TileWorldCreator component  
![tileWorldCreator](img/tileWorldCreator.png)  
  
The TileWorldCreator component is the main component and is responsible for executing the blueprint and build layer stacks.
By referencing the TileWorldCreator component you'll also get access to various runtime methods.  

+ `World name`  
  The name of the world game object where all layers, clusters and tiles are being parented.  
  Use different names if you have multiple TileWorldCreator components in one scene.  
+ `Map width` `Map height`  
  The size of the map  
+ `Cell size`  
  The size of a single cell  
+ `Map orientation`  
  The orientation of the map in the world (XZ or XY)  
+ `Custom random seed`  
  When enabled you can set a custom random seed which will be used for generating the map  
+ `Merge preview textures`  
  When enabled, the preview thumbnail textures will be merged with the preview texture from the last layer.  
+ `Use custom cluster cell size` 
  TileWorldCreator partitions the map into clusters. Instantiatd tiles and objects are being assigned to these clusters. Normally TileWorldCreator creates the cluster size based on the map size automatically. But it's possible that in some use cases the cluster size might be to large, especially on larger maps.  
  Please be aware that, the smaller the cluster size is, the longer it'll take to instantiate the tiles and objects.    
  > for more information please refer to [Merging&Clusters](/Workflow.md#merging)  
