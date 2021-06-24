# Concept & Workflow

## Concept
Because TileWorldCreator only requires four tiles to create beautiful tile maps, it is important to know how TileWorldCreator handles a map internally.
The generation stack handles a map by its original size but after generation is completed the map needs to be subdivided in order to be able to place the tiles correctly without creating single lost tiles which would result in open unclosed maps. See images below:

![tileError](img/tileError.png)  
**Error single tile**

![tileOk](img/tileOk.png)  
**Subdivided map with no error**    

> In the end this means that the size of a final instantiated map will always be two times the size of the width and height. Example: original size: 10x10 = 20x20 in unity units.


## Layers stack

### Generation Layers
TileWorldCreator consists of two different layer stacks. The first one is the **Generation layer stack**. Each layer in the generation stack consists of different actions called **generators** (cellular automata, maze, L-System etc.) or **modifiers** (copy, expand, smooth etc.). These will generate and modify your map.
TileWorldCreator executes the layers including their generators and modifiers from top to bottom.
So it is always wise to create your `base` map as the first layer and every additional modifications which depends on the `base` layer comes after it.


### Generation layer actions stack
IMAGE  
> Each generation layer executes each action in the action stack from top to bottom.  

**Example for a stack:**  
- Base layer
1. `Cellular Automata` Generate a new map with a cellular automata generator
2. `Smooth` Modify the map by smoothing it
- Inner layer
1. `Copy` copy the base map to the inner layer
2. `Shrink` shrink the map by one tile 
3. `Smooth` smooth the map a bit

## Instantiation Layers
Next we have the instantiation layer stack. These layers are responsible for taking the final output of your generated map from the generation layers stack and use it to instantiate your tiles or objects.
> Make sure the generation layers stack has been executed first before trying to execute the instantiation layers. 

### Merging & Clusters
An instantiation layer takes care of partitioning a map into smaller clusters. Each cluster contains multiple tile objects. When merging is enabled, all tiles inside of a cluster are being merged together.  When changing a map - by painting tiles for example - the instantiation tiles layer checks for all changed tiles in each cluster and updates only the changed cluster. 
> When creating large maps it is highly recommended to enable merging. 

### Instantiate Tiles
The instantiate tiles layer takes a TileWorldCreator tiles preset and automatically instantiates the tiles according to the assigned map. It also takes care of the correct rotation of the tiles. Depending on how you have exported your tiles from your 3d software you might need to adjust the rotation offset. 

#### Tiles preset
You can assign multiple tiles preset to a single tiles instantiation layer and set a random weight. This is great if you want to add some variety between tile sets. 

#### Ignore layers
Ignore layers can be used if you want to skip instantiation for tiles from another generation layer which overlaps with the assigned one. 
Example:
Here we have a map which has two height layers. The generation stack consists of two layers, one which generates the ground and another with an inset which generates the top level. Because of this, we don't want to instantiate the tiles in the ground layer which are underneath the top layer. Therefore we assign the top layer to the ignore layers. 

### Instantiate Objects



## Execute layers

> You can either execute each layer separately, the complete generation/instantiation stack or all layers together by clicking on the appropriate buttons.
