# FAQ

## All tile materials are pink what can I do?
All Tile preset materials are using the built-in RP.  
If you're using URP or HDRP you can simply upgrade those materials in your project by selecting:  

+ URP  
  `Edit / Render Pipeline / Universal Render Pipeline / Upgrade Project Materials to UniversalRP Materials`
+ HDRP  
  `Edit / Render Pipeline / HD Render Pipeline / Upgrade Project Materials to HDRP Materials`

## Nothing happens when I press the execute buttons?
Try holding the Left-CTRL key while clicking on the execute button to force a complete rebuild of the map.  

## Can I use TileWorldCreator for my 2d game?
TileWorldCreator does currently not support the official Unity 2D workflow (2D sprites & Tilemaps).  
But you can still use it for your 2D game, by using quad meshes with a textures on it as your 2D tiles.  
TileWorldCreator also supports XZ and XY map orientation.  
Support for 2D sprite and Tilemaps is currently under research.  

## How do I add ramps?
There are multiple ways of adding ramps. Either by adding a second tileset with ramps and randomly choose between the base tileset and the ramps tileset,  
or by adding single ramp objects by using a build objects layer.  
Please have a look at the 09_Ramps demo scene.  


## Does TileWorldCreator require API .Net 4.x like version 2.0?
No TileWorldCreator v.3 doesn't require API level .Net 4.x  

## Can I have more than one map in a scene?
Yes absolutely. Simply make sure to define an unique `World name` in the TileWorldCreator component.  

## Is the source code included?
Yes.

