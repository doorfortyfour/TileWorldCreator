# Workflow

## Generation Layers
TileWorldCreator consists of two different layer stacks. The first one is the **Generation layer stack**. Each layer in the generation stack consists of different actions called **generators** (cellular automata, maze, L-System etc.) or **modifiers** (copy, expand, smooth etc.). These will generate and modify your map.
TileWorldCreator executes the layers including their generators and modifiers from top to bottom.
So it is always wise to create your `base` map as the first layer and every additional modifications which depends on the `base` layer comes after it.

### Generation layer
IMAGE

### Generation layer actions stack
IMAGE  
> Each generation layer executes each action in the action stack from top to bottom.  

**Example for a stack:**  
1. `Cellular Automata` Generate a new map with a cellular automata generator
2. `Smooth` Modify the map by smoothing it


## Instantiation Layers
Next we have the instantiation layer stack. These layers are responsible for taking the final output of your generated map from the generation layers stack and use it to instantiate your tiles or objects.

### Instantiate Tiles


### Instantiate Objects



### Execute layers

> You can either execute each layer separately, the complete generation/instantiation stack or all layers together by clicking on the appropriate buttons.
