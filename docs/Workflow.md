# Concept & Workflow

## Concept
TileWorldCreator only requires four tiles to create tile maps.
Therefore it is important to know, how TileWorldCreator handles a map internally.
Each blueprint layer, including its generators and modifiers, handles a map by its original size. After generation is completed, the map is being subdivided in order to be able to place the tiles correctly without creating single lost tiles, which would result in unclosed maps. See images below:

![tileError](img/tileError.png) ![tileOk](img/tileOk.png)    

> In the end this means, that the size of a final instantiated map will always be two times the size of the width and height. So a map with the size of 10x10 will be the size of 20x20 unity units.

## TileWorldCreator component
![tileWorldCreator](img/tileWorldCreator.png)

The TileWorldCreator component is the main component and is responsible for executing the blueprint and build layer stacks.
By referencing the TileWorldCreator component you'll also get access to various runtime methods.

+ `Map width` `Map height`  
  The size of the map
+ `Cell size`  
  The size of a single cell  
+ `Map orientation`  
  The orientation of the map in the world (XZ or XY)  
+ `Use random seed`  
  When enabled you can set a custom random seed which will be used for generating the map  
+ `Merge preview textures`  
  When enabled, the preview thumbnail textures will be merged with the preview texture from the last layer.  
+ `Use custom cluster cell size` 
  TileWorldCreator partitions the map into clusters. Instantiatd tiles and objects are being assigned to these clusters. Normally TileWorldCreator creates the cluster size based on the map size automatically.  
  But it's possible that in some use cases the cluster size might be to large, especially on larger maps.
  Please be aware that, the smaller the cluster size is, the longer it'll take to instantiate the tiles and objects.  
  > for more information please refer to [Merging&Clusters](/Workflow.md#merging)  

## Blueprint Layers

![generationLayer](img/generationLayer.png)

TileWorldCreator consists of two different layer stacks. The `Blueprint layers` stack and the `Build layers` stack. Each layer in the blueprint layer stack has its own actions stack. These actions are called `generators` (cellular automata, maze, L-System etc.) or `modifiers` (copy, expand, smooth etc.). By combining those actions and layers you can easily create different "parts" of your map.
TileWorldCreator executes the layers including their generators and modifiers from top to bottom.
So it is always wise to create your `base` map as the first layer and every additional modifications which depends on the `base` layer comes after it.

![generationLayer](img/exampleBaseLayer.png)

+ `Layer Name`  
  The actual layer name  
+ `Color`  
  The color which should be used for the preview thumbnail texture  
+ `Stack`  
  The action stack of this specific layer  

### Actions stack  
![actionStack](img/actionStack.png)
> Each blueprint layer executes each action in the action stack from top to bottom.  

<br><br>
**Example for a stack:**  
#### Base Layer:
![baseLayer](img/exampleBaseLayer.png)
+ `Cellular Automata`  
  Generate a new map with a cellular automata generator
+ `Smooth`  
  Modify the map by smoothing it

#### Inner Layer:
![innerLayer](img/exampleInnerLayer.png)
+ `Add`  
  Add the base map to the new inner layer
+ `Shrink`  
  shrink the map by one tile 


## Build Layers
Next we have the build layers stack. Build layers are responsible for taking the final output of a blueprint layer and uses it to instantiate either tiles or objects.
> Make sure the blueprint layers stack has been executed first before trying to execute the build layers. 

### Build tiles Layer
The build tiles layer takes a TileWorldCreator tiles preset and automatically instantiates the tiles based on the assigned blueprint layer. It also takes care of the correct rotation of the tiles. Depending on how you have exported your tiles from your 3d software you might need to adjust the rotation offset. 

![instantiationLayerTiles](img/instantiationLayerTiles.png)

+ `Layer Name`  
  The layer name  
+ `Blueprint Layer`  
  The blueprint layer it should use for instantiation  
+ `Global Position offset` `Global scaling offset`  
  Add an additional transform offset to a single tile  
+ `Merge tiles`  
  Merge tiles in to clusters  
+ `Collision type`  
  Select between **None**, **Mesh Collider** and **Tile Collider**  
  + `None` Do not add any collision  
  + `Mesh Collider` Add the exact merged tile mesh as a mesh collider  
  + `Tile Collider` Generate a new mesh collider based on the tiles bounding box.  
    `Collider height` The collider height.  
    `Collider border offset` Add a border offset to the collision mesh, this is sometimes needed if border tiles do not "fill" the whole cell.  
  
+ `Tiles Presets`  
  You can assign multiple tiles preset to a single tiles instantiation layer and set a random weight. This is great if you want to add some variety between tile sets.  
+ `Ignore layers`  
  Ignore layers can be used if you want to skip instantiation for tiles from another blueprint layer which overlaps with the assigned one.  
  **Example:**  
  ![ignoreLayersExample](img/ignoreLayersExample.png)
  Here we have a map which has two blueprint layers `Base` and `Inner`. The `Base`layer generates the ground and the `Inner` layer shrinks the base layer by one tile to create the inner "grass" map. Because of this, we don't want to instantiate the tiles in the `Base` layer which are overlapping with the `Inner` layer. Therefore we assign the `Inner` layer to the ignore layers of the `Cliffs` build layer. 

### Tiles preset
![tilesPreset](img/tilesPreset.png)  
Tiles are stored in a separate asset file (scriptable object). This has the advantage of being able to reuse tile presets 
in different TileWorldCreator assets.
#### Create a Tiles Preset
1. Right click in the project view and select `Create / TileWorldCreator / New TileWorldCreator Tiles preset`
2. Assign your tiles based on their type 
+ ![edgeTile](img/edgeTile.png) `Edge`  
+ ![exteriorCornerTile](img/exteriorCornerTile.png) `Exterior Corner`    
+ ![interiorCornerTile](img/interiorCornerTile.png) `Interior Corner`  
+ ![fillTile](img/fillTile.png) `Fill`  


### Build objects layer
![instantiationLayerObject](img/instantiationLayerObjects.png)  
The build objects layer instantiates single prefabs based on the assigned blueprint layer.
  
+ `Name`  
  The layer name  
+ `Blueprint layer`  
  The blueprint layer it should use for instantiation  
+ `Use subdivided map`  
If true, objects will be placed similiar to tiles by using the subdivided map. That means for a 1x1 cell it will place 2x2 objects.  
If this is not desired leave it off.  
+ `Position offset` `Rotation offset` `Scale offset`  
  Add an additional transform offset to the object  
+ `Childs`  
  When enabled you can assign an additional child object which will be instantiated in a certain radius around the parent object.  
+ `Random Position` `Random Rotation` `Random Scaling`  
  Modifies the objects transform by random values.  
+ `Merge`  
  Merge the instantiated objects in to clusters.  

## Merging & Clusters :id=merging
A build layer takes care of partitioning a map into smaller clusters. Each cluster contains multiple tile objects. When merging is enabled, all tiles inside of a cluster are being merged together.  When changing a map - by painting tiles for example - the build tiles layer checks for all changed tiles in each cluster and updates only the changed cluster. 
> When creating large maps it is highly recommended to enable merging. 


## Execute layers

> You can either execute each layer separately, the complete blueprint/build stack or all layers together by clicking on the appropriate buttons.
