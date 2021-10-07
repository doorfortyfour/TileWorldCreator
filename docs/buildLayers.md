## Build Layers
Build layers are responsible for instantiating prefabs (tiles, objects) based on their assigned blueprint layer. 
There are currently three different build layers:  

+ 3D 4-Tiles
+ 3D 6-Tiles
+ Objects


## 3D 4-Tiles && 6-Tiles build layers
IMAGE
The build layers takes a TileWorldCreator tile-preset and automatically instantiates the tiles based on the assigned blueprint layer. It also takes care of the correct rotation of the tiles. Depending on how you have exported your tiles from your 3d software you might need to adjust the rotation offset. 

### 4-Tiles  
![4tiles](img/new4Tiles.png)  
A 4-Tiles build layer uses only four tiles to build a complete map. Therefore tiles needs at least 2 adjacent neighbouring tiles to make sure that the map is completely "closed". This means that the assigned blueprint map will be subdivided and a instantiated tiles should be half the size of the cell size.  
> It is recommended to enable `Scale tile by cell size` in the build layer


### 6-Tiles  
![6tiles](img/new6Tiles.png)  
A 6-Tiles build layer uses six tiles. It can be used for creating path like structures like roads, fences, pipes, rivers etc.  


![instantiationLayerTiles](img/buildLayer.png)

+ `Layer Name`  
  The layer name  
+ `Blueprint Layer`  
  The blueprint layer it should use for instantiation  
+ `Scale tile by cell size`  
  Scale the tile automatically based on the cell size. This works only reliable if your tile prefab has a size of 1x1 units
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
  You can assign multiple tiles preset to a single tiles build layer and set a random weight. This is great if you want to add some variety between tile sets.  
+ `Ignore layers`  
  Ignore layers can be used if you want to skip instantiation for tiles from another blueprint layer which overlaps with the assigned one.  
  **Example:**  
  ![ignoreLayersExample](img/ignoreLayersExample.png)
  Here we have a map which has two blueprint layers `Base` and `Inner`. The `Base`layer generates the ground and the `Inner` layer shrinks the base layer by one tile to create the inner "grass" map. Because of this, we don't want to instantiate the tiles in the `Base` layer which are overlapping with the `Inner` layer. Therefore we assign the `Inner` layer to the ignore layers of the `Cliffs` build layer.  
  
  
## Tiles preset
![tilesPreset](img/tilesPreset.png)  
Tiles are stored in a separate asset file (scriptable object). This has the advantage of being able to reuse tile presets 
in different TileWorldCreator assets.

  + `Rotation offset` Depending on how your tiles have been created in your 3D software, you will have to add a rotation offset.
  + `Scaling offset` Add a scaling offset to a single tile. Often used when changing the cell size (!=1)

#### Create a Tiles Preset
1. Right click in the project view and select `Create / TileWorldCreator / New 3D Tiles preset`
2. Assign your tiles based on their type 
+ ![edgeTile](img/edgeTile.png) `Edge`  
+ ![exteriorCornerTile](img/exteriorCornerTile.png) `Exterior Corner`    
+ ![interiorCornerTile](img/interiorCornerTile.png) `Interior Corner`  
+ ![fillTile](img/fillTile.png) `Fill`  


### Build objects layer
![instantiationLayerObject](img/instantiationLayerObjects.png)  
The build objects layer instantiates single prefabs based on the assigned blueprint layer.  
Can be used for placing trees, props or even enemies or the player character itself.
  
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

You can either execute each layer separately, the complete blueprint/build stack or all layers together by clicking on the appropriate buttons.
> Hold the Left-CTRL key while clicking on one of these buttons to force a complete rebuild of the map.
