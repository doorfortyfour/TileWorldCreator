# Custom action
In TileWorldCreator, an action is either a generator or a modifier. The main difference between a generator and a modifier is, that a generator is basically a function/algorithm which creates a map from scratch, while a modifier modifies an existing map and returns the modified map. 
You can easily create your own custom actions for TileWorldCreator, read further to see how.  

## Template
> Simply use this template code to create your own action.




Make sure the class inherits from `TWCBlueprintAction` and implements the `ITWCAction` interface.  
Then you can add your custom map modification code inside of the `Execute` method and return the modified map.  
All custom GUI code should be inside of the `DrawGUI` method.  
