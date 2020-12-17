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

### Matplotlib: plt v.s. ax
 - [What Are the “plt” and “ax” in Matplotlib Exactly?](https://towardsdatascience.com/what-are-the-plt-and-ax-in-matplotlib-exactly-d2cf4bf164a9)
 - ![](https://miro.medium.com/max/1338/1*zxvxtqmcl9rFVj5yN4pNjA.png)
 - If you only want to draw one graph, both are acceptable; If you want to draw multiple graphs, then you almost certainly want to use `ax`.
 - `plt` creates a `figure` object and an `axes` object inside `figure` object. 
 - `plt.subplots()` returns the `figure` object and the `axes` object so that we could do more things to them.