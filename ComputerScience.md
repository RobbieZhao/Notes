# Notes for CS

### Delegation v.s. inheritance

 - Delegation means passing the duty to another class. 
 - When you want to "copy" and expose the base class' API, you use inheritance. When you only want to "copy" functionality, use delegation. [When to use delegation instead of inheritance?](https://stackoverflow.com/questions/832536/when-to-use-delegation-instead-of-inheritance)


### [Implications of functional programming](https://www.youtube.com/watch?v=wO83CH3MK9o&list=PLbdXd8eufjyW-EwjND9IqwI8rvpsfUgRZ&index=1) 
 - functional programming is avoiding state. The alternative: imperative programming
 - functional programming often means functions as values. The alternative: first-order programming
 - functional programming often means datatype-oriented programming. The alternative: object-oriented programming
   - datatype-oriented: call an operation with an variant
     - new operation => new function
     - new variant => change all the functions
   - object-oriented: call a variant with an operation
     - new operation => change all objects
     - new variant => new objects
   - these tradeoffs are the fundamental differences between datatype-oriented programming and object-oriented programming

### Some rules of functional programming
 - [Learning Functional Programming with JavaScript - Anjana Vakil - JSUnconf](https://www.youtube.com/watch?v=e-5obm1G_FY)
 - Express everything as functions: takes an input and gives an output
 - Avoid side effects: use pure functions
 - Don't iterate. Use map, reduce, and filter.
 - Avoid mutation: persistent data structures for efficient immutability.

