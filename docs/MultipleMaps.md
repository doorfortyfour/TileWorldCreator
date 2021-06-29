# Multiple Maps

TileWorldCreator creates an empty game object where all clusters and tile objects are being parented to.
It is possible to have multiple TileWorldCreator instances in one scene, for example if you want to have different kind of maps.
To make sure that another instance of a TileWorldCreator component doesn't use the same game object for parenting, you'll need
to change the `World name` on the TileWorldCreator component. 

## Transforms

A map can be moved by the transforms of the game object where the TileWorldCreator component is assigned to.
