# Run Once JS Decorator

Run Once JS Decorator is a js function that ensures that your function run once.

# What does it look like?

It's look like a python decorator, but without @.

Python uses:
    @dec
    def my_func(params):
        #Code

### **Code**:

This is all code that you have to put before your function:

    var decRunOnce = function(func){
        var newFunc = function(){
            if (!arguments.callee.runned){
                arguments.callee.runned = true;
                func.apply(this, arguments);
            }
        };
        newFunc.runned = false;
        newFunc.reset = function(){
            newFunc.runned = false;
        };
        return newFunc;
    };

### Usage:

    - Put the code before your function.
    - Call it passing your function.
    - The return will be your function that can exec once.

### Example:

    <!-- Call the decorator -->
    var decRunOnce = function(func){
        var newFunc = function(){
            if (!newFunc.runned){
                newFunc.runned = true;
                func.apply(this, arguments);
            }
        };
        newFunc.runned = false;
        newFunc.reset = function(){
            newFunc.runned = false;
        };
        return newFunc;
    };
    
    
    /* User Function */
    function myFunction(arg){
        console.log(arg);
    }
    myFunction('a'); /* show on console => a */
    myFunction('a'); /* show on console => a */
    myFunction('c'); /* show on console => c */
    myFunction('z'); /* show on console => z */
    myFunction('foo'); /* show on console => foo */
    
    /* Now you call Run Once Decorator on your function. */
    myFunction = decRunOnce(myFunction);
    myFunction('b'); /* show on console => b */
    myFunction('b'); /* Do nothing */
    myFunction('c'); /* Do nothing */
    myFunction('bar'); /* Do nothing */
    myFunction('foo'); /* Do nothing */
    myFunction('foobar'); /* Do nothing */
    myFunction('b'); /* Do nothing */
    myFunction('b'); /* Do nothing */
    
    myFunction.reset(); /* now you can run once your function */
    myFunction('bar'); /* show on console => bar */
    myFunction('c'); /* Do nothing */
    myFunction('bar'); /* Do nothing */
    myFunction('foo'); /* Do nothing */
    myFunction('c'); /* Do nothing */
    