
Chip:

Core (processor)

Great Ideas in Computer Architecture

 - Abstraction: hiding details from the upper level
 - Moore's Law: design through trends
 - Principles of locality: programs are predictable
 - Parallelism: 
 - Performance Measurement & Improvement
 - Dependability vs redundancy: a failing piece doesn't make the whole system fail

Storage latency

 - register: 1 ns
 - on chip cache: 2
 - on board cache: 10
 - memory: 100
 - disk: 10^6
 - tape/optical robot: 10^9

Everything is a number

Two's complement:
 - Most significant: left most bit
 - least significant: right most bit
 - To get negative number: invert all bits and add 1
 
How to know if there is an overflow?

 - If the carry in and carry out of the most significant bit are the same, then there is overflow.
 - If they are not the same, then there is an overflow.
 - overflow: numbers are too large to represent
 - underflow: numbers are too small to represent

C is a compiled language

 - compilation: compiles C programs into architecture-specific machine code
   - java: converts java code into architecture-independent bytecode
 - compilation process:
   - `.c` -> cpp -> `.i` -> compiler -> `.s` -> assembler -> `.o` (object code files) -> linker -> `a.out`
 - fast: optimizes for a given architecture
 - use underscores for naming
 - when c program starts:
   - executable is loaded into memory
   - OS sets up the stack, then calls into C runtime library
   - runtime library initializes memory and other libraries
   - then calls main

C grammars:

 - int: word size, the size that target processor work with most efficiently
 - sizeof(long long) >= sizeof(long) >= sizeof(int) >= sizeof(short)
   - short >= 16 bit
   - long >= 32 bits
 - pointer: A variable that contains the address of a variable
 - C passes by value

IEC prefix system

 - Ki: 2<sup>10</sup>
 - Mi: 2<sup>20</sup>
 - Gi: 2<sup>30</sup>
 - Ti: 2<sup>40</sup>
 - Pi: 2<sup>50</sup>
 - Ei: 2<sup>60</sup>
 - Zi: 2<sup>70</sup>
 - Yi: 2<sup>80</sup>

C grammars

 - `void*` is a type that can point to anything
 - any variable declared inside a function that is not defined can be any value
 - C structure assignment is not a deep copy. All members are copied, but not things pointed to by members 
 - arrays
   - int arr[2];
   - int arr[] = {1, 2};
 - array variable almost identical to pointers
 - accessing out of bound array elements: segmentation fault or bus errors
 - DRY: don't repeat yourself
 - the number of bits in a byte is not standardized
 - avoid using pointer arithmetic
 - endianness of arrays?
 - C defines the one element past end of array must be a valid address

C address space

 - stack: goes down. Variables declared inside a function.
 - heap: does up.  Dynamically allocated data.
 - static data: data statically known. Variables declared outside functions, does not grow or shrink.
 - code

The stack

 - includes:
   - return address
   - arguments
   - space for local variables

The heap

 - malloc: allocate a block if uninitialized memory
   - `void *malloc(size_t n)`
   - size_t: a kind of unsigned integer that is guaranteed to count all the bytes in memory
   - returns a void*. returns NULL if no more memory.
   - use sizeof in the argument value to produce more portable code
 - calloc: allocate a block is zeroed memory
 - free: free previously allocated memory
   - `void free(void *p)`
 - cfree: don't use it
 - realloc: change size of previously allocated block (it may move)

 Brian Harvey's C notes
 
  - page 12: int i
    - allocation for local variables happens while the program is running, but memory for global variables is allocated as part of the compilation process

C grammars:

 - ~ bitwise not
 - ! 0 -> 1; non-zero -> 0
 - ^ xor. return 1 if different, 0 otherwise. exclusive or is commutative and associative
 - / round towards 0

GDB

 - compile with -g option
 - commands:
   - b n: set breakpoint at line n
   - break n if expr: set breakpoint is expr is true
   - run [arglist] run the program
   - n step over
   - s step into
   - c continue running the program
   - p expr show value of an expression
   - display expr show value of an expression each time program stops

ISA: Instruction Set Architecture

 - The set of instructions a particular CPU implements

RISC: Reduced Instruction Set Computing

 - Keep the instruction set small and simple, makes it easier to build fast hardware
 - let softwares do complicated operations by composing simpler ones

MIPS:

 - 32 registers, each register is 32 bits wide (a word)
   - numbered from 0-31: `$0-$31`
   - `$16-$23` or `$s0-$s7`: correpond to c variables
   - `$8-$15` or `$t0-$t7`: temporary variables
   - registers have no type: operation determines how register contents are treated
 - addition: `add $s0,$s1,$s2` == `a = b + c`
 - subtraction: `sub $s3,$s4,$s5` == `d = e - f`
 - a = b + c + d - e

        add $t0,$s1,$s2
        add $t0,$t0,$s3
        sub $s0,$t0,$s4
 - comment: `#`
 - immediate: numerical constants
   - `addi $s0,$s1,-10` == `f = g - 10`
 - `add $s0,$s1,$zero` == `f = g`
 - add, addi, sub cause overflow to be detected. addu, addiu, subu do not cause overflow detection
   - MIPS C compilers produce addu, addiu, subu
 - big-endian
 - `int A[100]; g = h + A[3]`
   - `lw $t0,12($s3)`
   - `add $s1,$s2,$t0`
 - `int A[100]; A[10] = h + A[3]`
   - `lw  $t0,12($s3)`
   - `add $t0,$s2,$t0`
   - `sw  $t0,40($s3)`
 - load byte: `lb`
   - `lb $s0,3($s1)` load the byte into the low byte position of `$s0`, and sign-extend the byte (if the first bit of the byte is 1, fill the rest with 1, 0 otherwise)
   - `lbu` unsign-extend
 - store byte: `sb`
 - bitwise operations: and, or, not
 - logic shifting: sll, srl
   - `sll $s1,$s2,2` == `s1 = s2 << 2` (inserting 0 on the right)
   - `srl` (insert 0 on the left)
 - arithmetic shifting
   - `sra` insert high order sign bit on the left
 - `beq`: branch if equal
   - beq register1,register2,L1
   - go to statement labeled L1 if value in register1 == value in register2
 - `bne`: branch if not equal
 - unconditional branch: `jump/j`