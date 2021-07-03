# Custom action
In TileWorldCreator, an action is either a generator or a modifier. The main difference between a generator and a modifier is, that a generator is basically a function/algorithm which creates a map from scratch, while a modifier modifies an existing map and returns the modified map. 
You can easily create your own custom actions for TileWorldCreator, read further to see how.  

## Custom generator
To create a custom action of type generator follow these steps.  

1. Create a new class  
2. Inherit from the base class TWCAction  
3. Implement the interface ITWCAction   
4. Override following methods  
5. Create the execute code  
6. Create the custom gui code  
7. Add the class attribute  

## Custom modifier
