![test](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/postman.jpg)

# Summary

This collection shows how to reset the  variables values at the end of the collection execution.

# Description

Some times collection run might modify environment variables or collection variables and you want to reset these to the initial value each time the collection run completes. 

Here we takes the initial values and store it in a variable and then replaces the variable values with the initial value at the end of the collection run. 


![warning](https://thumbs.gfycat.com/SlimyConcernedBlackfish-size_restricted.gif)
**Important** if you don't want variable modification to reflect after the collection run, use pm.variables.set as it creates local variables that have lifetime of collection run. After that it gets destroyed.

It also has more precedence so if a collection and local variable exists , then value is taken from local variable.

**THis collection is just to show that you can do variable reset from postman** but the right practice is to use pm.variables

# Usage instruction

Just run the collection using newman or collection runner , try enabling and disabling the test script and see the behavior