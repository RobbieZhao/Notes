 - The return type of `main` has to be `int`
 - check [GCC manual](https://gcc.gnu.org/onlinedocs/) to find the default standard of C++
 - `#include` directive must appear outside any function
 - `::` scope operator
 - Headers from the standard library are enclosed in angle brackets `< >`. Those that are not part of the library are enclosed in double quotes `" "`

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