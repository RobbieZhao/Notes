Compilation of C programs:

 - Preprocessing
   - removing comments
   - expanding macros
   - expanding included files
 - Compiling: generates assembly language
 - Assembly: convert assembly code into binary code
 - Linking
   - static linking
   - dynamic linking

Scope vs extent:

 - scope: where in the program this variable is available for use
 - extent: how long it exists

**[Datatypes in C](https://en.wikipedia.org/wiki/C_data_types)**

 - Basic types in C
   - `char` a single byte
   - `int` word size, the size that target processor work with most efficiently
   - `float` 
   - `double`
 - short and long apply to integers
   - `sizeof(long long)` >= `sizeof(long)` >= `sizeof(int)` >= `sizeof(short)`
   - short >= 16 bits
   - long >= 32 bits
 - signed or unsigned can be applied to char or any integer
   - whether chars are signed or unsigned, printable chars are always positive
 - long can be applied to long double
 - In C, unsigned integer overflow is defined to wrap around, while signed integer overflow causes undefined behavior.
 - C does not define how many bits are in a byte
 - [float specifiers](https://stackoverflow.com/questions/34706228/difference-between-upper-and-lower-case-double-float-type-specifiers-in-c)
 - The C standard doesn't define how many bits are in a float or double: [link](https://stackoverflow.com/questions/25524355/what-is-the-size-of-float-and-double-in-c-and-c)

**Bitwise operations**

 - `~` bitwise not
 - `!` 0 -> 1; non-zero -> 0
 - `^` xor. return 1 if different, 0 otherwise. exclusive or is commutative and associative