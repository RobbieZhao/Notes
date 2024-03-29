 - c++ is a statically typed language: the types are checked at compile time
 - The return type of `main` has to be `int`
 - check [GCC manual](https://gcc.gnu.org/onlinedocs/) to find the default standard of C++
 - `#include` directive must appear outside any function
 - `::` scope operator
 - Headers from the standard library are enclosed in angle brackets `< >`. Those that are not part of the library are enclosed in double quotes `" "`


## Variables
 - initialization is not assignment
   - initialization: a variable is given a value when it is created
   - assignment: obliterates an object's current value and replaces that value with a new one
 - uninitialized variables
     - built-in type
       - outside any function: initialized to zero
       - inside a function: uninitialized (undefined)
     - class: depends on the class
 - it is an error to provide an initializer on an extern inside a function
 - `::name` fetch the name on the right hand side from the global scope (the global scope has no name)
 - declaration: 
   - base type
   - declarators: names a variable and gives the variable a type that is related to the base type
 - A reference must be initialized
 - It is illegal to assign an int variable to a pointer, even if the variable's value happens to be 0

        int *p = 0;     // OK equivalent to int *p = nullptr
        int zero = 0;
        int *p = zero   // Error   
 - const
   - reference to const: cant change the object through the reference
   - pointer to const: cant change the object througth the pointer
   - const pointer: cant change the pointer itself.
 

## `iostream` library

 - two types
   - `istream`
     - `cin`: standard input
   - `ostream`
     - `cout` standard output
     - `cerr`: warning and error messages
     - `clog`: general info about the execution of a program
 - The system associates each of these objects with the window in which the program is executed
 - `std::endl` is a special value called a manipulator. When written,, manipulates the stream
   - std::cout << std::endl has the effect of ending the current line and flushing the buffer associated with the device
   - reading `std::cin` flushes `std::cout`
   - `std::cout` is also flushed when the program ends normally. 
   - `std::cout` can flush the buffer at any time. but when using g++ it doesn't flush the buffer
 - `<<` output operator. Writes the rhs on the `ostream` object.
   - `std::cout << "hello world"` returns it left hand operand
 - `>>` input operator. Reads data from the given`istream` and stores what was read in the rhs