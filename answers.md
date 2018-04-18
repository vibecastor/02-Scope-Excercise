##Questions:
1. When this code is run in Node, e.g. node index.js, what are the two stages of execution for this file called, and which order do they happen in?

- First the code will be compiled and then it will be executed (actually run by the engine).

2. Write an explanation, using as much space as you need, relating to how the first stage of execution for this file operates.

- During code compilation the complier will first tokenize the code breaking the code which is presented as string data into meaningful chunks.  Then Parsing takes all the chunks of data stored as an array of strings and turns them into a tree structure known as an "AST" or Abstract Syntax Tree.  The compiler looks for bindings performing 'hoisting' where bindings including functions are 'hoisted' to the top of their scopes. The complier stores bindings by performing "lhs" or left-hand-side lookup ups finding declared bindings (example:  Var foo; ).  The complier will also determine each bindings scope as it was declared at author time.


3. Write an explanation, using as much space as you need, relating to how the second stage of execution for this file operates.

- During execution, the javascript engine will run the code,  
performing right-hand-side look ups to find the assigned values of the previously hoisted bindings (example:  foo = "bar" in the scope of 'baz').  The engine will run function calls as they were created in author time.  The function calls run on something called a "stack" which is a data structure that explains how functions run inside the engine.  The currently running function would be said to be on the top of the stack. Once a function is done running it would be moved to 'garbage collection' which is how the engine recovers memory for use in future operations.

4. During the second stage of execution how many scopes have been registered by the engine?

- Which segments of the code do they belong to?
  - There are three scopes in this particular code example, global scope, function scope for bar(); and function scope for baz();

- Please identify any variables/refs and which scope each belongs to?
  - Global:  var foo = 'bar' and function bar() has access to the global scope.
  - Scope of bar() contains references to var foo = 'baz'; function baz()
  - Scope of baz() contains references to a parameter (foo) as well as foo = 'bam'; and bam = 'yay';

5. When line 13 invokes the baz function, which foo will be assigned a value of bam? More specifically, bam will be assigned to the foo in ??? scope. Give a brief description in your own words to support your conclusion.
- foo will be assigned a value of "bam" from inside the scope of baz() because binding assignment is predicated by run-time meaning that if baz() is firing then foo's value will come from inside of baz();  

6. Which scope, if any, will the variable bam on line 11 be registered to when the first stage of execution occurs on this file? Provide a brief description in your own words to support your conclusion.
- the locally scoped binding "bam" will produce a "ReferenceError".  The engine will attempt to hoist it to the global scope but in 'strict mode' undeclared variables produce a ReferenceError.

7. For each line, 16 through 19, what is the return value for each?
- bar(); returns a "ReferenceError" 
- foo; //returns "bar"
- bam; //returns a ReferenceError
- baz(); //returns a ReferenceError