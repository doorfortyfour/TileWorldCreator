# Concept & Workflow

## Concept
Because TileWorldCreator only requires four tiles to create beautiful tile maps, it is important to know how TileWorldCreator handles a map internally.
The generation stack handles a map by its original size but after generation is completed the map needs to be subdivided in order to be able to place the tiles correctly without creating single lost tiles which would result in open unclosed maps. See images below:

![tileError](img/tileError.png)  
**Error single tile**

![tileOk](img/tileOk.png)  
**Subdivided map with no error**    

> In the end this means that the size of a final instantiated map will always be two times the size of the width and height. Example: original size: 10x10 = 20x20 in unity units.



## Generation Layers

![generationLayer](img/generationLayer.png)

TileWorldCreator consists of two different layer stacks. The **Generation layers** stack and the **Instantiation layers** stack. Each layer in the generation layer stack consists of different actions called **generators** (cellular automata, maze, L-System etc.) or **modifiers** (copy, expand, smooth etc.). With these you can create and modify a map. Layers can be used to build different parts of your map with different tile presets or objects.
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
> Each generation layer executes each action in the action stack from top to bottom.  

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
+ `Copy`  
  copy the base map to the inner layer
+ `Shrink`  
  shrink the map by one tile 


## Instantiation Layers
Next we have the instantiation layers stack. These layers are responsible for taking the final output of a generated layer from the generation layers stack and use it to instantiate the tiles or objects.
> Make sure the generation layers stack has been executed first before trying to execute the instantiation layers. 

### Instantiate Tiles
The instantiate tiles layer takes a TileWorldCreator tiles preset and automatically instantiates the tiles based on the assigned layer. It also takes care of the correct rotation of the tiles. Depending on how you have exported your tiles from your 3d software you might need to adjust the rotation offset. 

![instantiationLayerTiles](img/instantiationLayerTiles.png)

+ `Layer Name`  
  The layer name  
+ `Assigned Layer`  
  The generated map layer it should use for instantiation  
+ `Global Position offset` `Global scaling offset`  
  Add an additional transform offset to a single tile  
+ `Merge tiles`  
  Merge tiles in to clusters  
+ `Add mesh collider`  
  Add a mesh collider to the merged mesh
+ `Tiles Presets`  
  You can assign multiple tiles preset to a single tiles instantiation layer and set a random weight. This is great if you want to add some variety between tile sets.  
+ `Ignore layers`  
  Ignore layers can be used if you want to skip instantiation for tiles from another generation layer which overlaps with the assigned one.  
  **Example:**  
  ![ignoreLayersExample](img/ignoreLayersExample.png)
  Here we have a map which has two height layers. The generation stack consists of two layers, one which generates the ground and another with an inset which generates the top     level. Because of this, we don't want to instantiate the tiles in the ground layer which are underneath the top layer. Therefore we assign the top layer to the ignore layers. 

### Instantiate Objects
The instantiate objects layer instantiates single prefabs based on the assigned generated layer.
  
+ `Name`  
  The layer name  
+ `Use layer`  
  The generated map layer it should use for instantiation  
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

## Merging & Clusters
An instantiation layer takes care of partitioning a map into smaller clusters. Each cluster contains multiple tile objects. When merging is enabled, all tiles inside of a cluster are being merged together.  When changing a map - by painting tiles for example - the instantiation tiles layer checks for all changed tiles in each cluster and updates only the changed cluster. 
> When creating large maps it is highly recommended to enable merging. 


## Execute layers

> You can either execute each layer separately, the complete generation/instantiation stack or all layers together by clicking on the appropriate buttons.
