## [CS61C Spring 2015](https://inst.eecs.berkeley.edu/~cs61c/sp15/)


Chip vs Processor vs Core

 - A processor can have multiple cores

**Great Ideas in Computer Architecture**

 - Abstraction: hiding details from the upper level
 - Moore's Law: design through trends
 - Principles of locality: programs are predictable
 - Parallelism
 - Performance Measurement & Improvement
 - Dependability vs redundancy: a failing piece doesn't make the whole system fail

**Storage latency**

 - register: 1 ns
 - on chip cache: 2
 - on board cache: 10
 - memory: 100
 - disk: 10^6
 - tape/optical robot: 10^9

Everything is a number

**Two's complement**

 - Most significant: left most bit
 - least significant: right most bit
 - To get negative number: invert all bits and add 1
 
**How to know if there is an overflow?**

 - If the carry in and carry out of the most significant bit are the same, then there is overflow.
 - If they are not the same, then there is an overflow.
 - overflow: numbers are too large to represent
 - underflow: numbers are too small to represent

**C grammars**

 - C is a compiled language
   - compilation: compiles C programs into architecture-specific machine code
   - java: converts java code into architecture-independent bytecode
   - fast: optimizes for a given architecture
 - use underscores for naming
 - when c program starts:
   - executable is loaded into memory
   - OS sets up the stack, then calls into C runtime library
   - runtime library initializes memory and other libraries
   - then calls main
 - pointer: A variable that contains the address of a variable
 - C passes by value

**IEC prefix system**

 - Ki: 2<sup>10</sup>
 - Mi: 2<sup>20</sup>
 - Gi: 2<sup>30</sup>
 - Ti: 2<sup>40</sup>
 - Pi: 2<sup>50</sup>
 - Ei: 2<sup>60</sup>
 - Zi: 2<sup>70</sup>
 - Yi: 2<sup>80</sup>

**C grammars**

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
 - C defines the one element past end of array must be a valid address
 - `/` round towards 0
 - C has two storage classes: automatic and static
   - automatic variables: local to function and discarded when function exits
   - static variables: exist across exits from and entries to procedures

**C address space**

 - stack: goes down. Variables declared inside a function.
 - heap: does up.  Dynamically allocated data.
 - static data segment: data statically known. Variables declared outside functions, does not grow or shrink.
 - code: text segment 
 - reserved area

**stack**

 - return address
 - arguments
 - space for local variables

**heap**

 - `malloc` allocate a block if uninitialized memory
   - `void *malloc(size_t n)`
   - `size_t` a kind of unsigned integer that is guaranteed to count all the bytes in memory
   - returns a `void*`. returns `NULL` if no more memory.
   - use `sizeof` in the argument value to produce more portable code
 - `calloc` allocate a block is zeroed memory
 - `free` free previously allocated memory
   - `void free(void *p)`
 - `cfree` don't use it
 - `realloc` change size of previously allocated block (it may move)


**Brian Harvey's C notes**
 
  - page 12: int i
    - allocation for local variables happens while the program is running, but memory for global variables is allocated as part of the compilation process

**GDB**

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

**ISA: Instruction Set Architecture**

 - The set of instructions a particular CPU implements

 - RISC: Reduced Instruction Set Computing
   - Keep the instruction set small and simple, makes it easier to build fast hardware
   - let softwares do complicated operations by composing simpler ones

**MIPS registers**

 - 32 registers, each register is 32 bits wide (a word), numbered from 0-31: `$0-$31`
   - `$16-$23` or `$s0-$s7` saved registers: correpond to c variables
   - `$8-$15` or `$t0-$t7`: temporary registers
   - `$0` or `$zero` zero register
 - registers have no type: operation determines how register contents are treated


**MIPS instructions**

 - each instruction is 4 bytes long
 - comment: `#`
 - MIPS assumes Big-Endian

**addition and subtraction of integers**

 - addition: `add $s0,$s1,$s2` == `a = b + c`
 - subtraction: `sub $s3,$s4,$s5` == `d = e - f`
 - add and subtract: `a = b + c + d - e`

        add $t0,$s1,$s2
        add $t0,$t0,$s3
        sub $s0,$t0,$s4
        
 - add immediate (numerical constants)
   - `addi $s0,$s1,-10` == `f = g - 10`
   - `add $s0,$s1,$zero` == `f = g`
   - `add`, `addi`, `sub` cause overflow to be detected. `addu`, `addiu`, `subu` do not cause overflow detection
   - MIPS C compilers produce addu, addiu, subu (most C implementations don't detect overflow)

**Transfer data between memory and registers**

 - transfer words `lw` `sw`
   - `int A[100]; g = h + A[3]`
     - `lw $t0,12($s3)`
     - `add $s1,$s2,$t0`
   - `int A[100]; A[10] = h + A[3]`
     - `lw  $t0,12($s3)`
     - `add $t0,$s2,$t0`
     - `sw  $t0,40($s3)`
 - transfer half word: `lh`
 - transfer bytes `lb` `lbu` `sb`
   - load byte: `lb`
     - `lb $s0,3($s1)` load the byte into the low byte position of `$s0`, and sign-extend the byte (if the first bit of the byte is 1, fill the rest with 1, 0 otherwise)
   - `lbu` unsign-extend
   - store byte: `sb`

**Logical instructions**

 - bitwise operations: `and`, `or`, `not`
 - shifting
   - logic shifting: `sll`, `srl`
     - `sll $s1,$s2,2` == `s1 = s2 << 2` (inserting 0 on the right)
     - `srl` (insert 0 on the left)
   - arithmetic shifting
     - `sra` insert high order sign bit on the left
 - set a register to be 0: `xor $s0,$0,$0`

**Control flow**

 - conditional branch: `beq`, `bne`
   - `beq`: branch if equal
     - `beq register1,register2,L1`
     - go to statement labeled L1 if value in register1 == value in register2
     - L1: the offset from the current instruction
   - `bne`: branch if not equal
 - unconditional branch
   - jump `j L1`
   - jump register `jr $ra`
     - put `$ra` into PC

**Inequality**

 - `slt` set on less than
   - `slt reg1,reg2,reg3`
     - `if (reg2 < reg3)`
     - `   reg1 = 1;`
     - `else reg1 = 0;`
   - set means change to 1
   - reset means change to 0
 - `sltu` treats registers as unsigned
 - `slti` immediate version of slt
   - `slti $t0,$s0,1`

**PC: program counter**

 - internal register inside the processor
 - instruction is fetched from memory, then control unit executes instruction using datapath and memory system, and updates program counter
 - processor
   - control
   - datapath
     - PC
     - registers
     - ALU: Arithmetic & Logical Unit

**Calling functions**

 - six fundamental steps
   - put parameters in a place where function can access them: copy the parameters into argument registers
   - transfer control to function
     - set up the return address `$ra`, jump to the function address
     - or `jal func` jump and link (jump and store the return address (the next instruction) into `$ra`)
   - acquire (local) storage resources needed for function (change `$sp`)
     - stack frame / procedure frame / activation record
     - segment of stack with saved registers and local variables
   - perform desired task of the function
   - put result value in a place (`$v0,$v1`) where calling code can access it and restore any registers you used
   - return control to point of origin, since a function can be called from several points in a program: `jr $ra`
 - registers
   - `$a0-$a3` (4-7) four argument registers to pass parameters
   - `$v0-$v1` (2-3) return value registers
   - `$ra` (31) return address register to return to the point of origin
   - `$sp` (29) the stack pointer
   - `$fp` (30) point to the first word of frame (if you don't know how big stack is gonna be when a function starts up, e.g. variable size of arrays)
   - `$gp` (28) global pointer, points to start of static data
 - two categories of registers
   - preserved across function call: caller can rely on values being unchanged: `$ra` `$sp` `$gp` `$fp` `$s0-$s7`
   - not preserved across function call: caller cannot rely on values being unchanged: `$v0,$v1` `$a0-$a3` `$t0-$t9`
 - data between `$sp` and `$fp`
   - saved argument registers (if any)
   - saved return address
   - saved saved registers (if any)
   - local arrays and structures (if any)

**MIPS instruction format**

 - I-format: instructions that have intermediates (except shift operations)
   - 6 opcode
   - 5 rs
   - 5 rt
   - 16 immediate
 - J-format: jump instructions
   - 6 opcode
   - 26 target address
 - R-format: all the other operations (operations that only operate on registers) (`jr`)
   - 6 opcode: partially specifies what instruction it is
   - 5 rs: register source
   - 5 rt: register target (another source)
   - 5 rd: register destination
   - 5 shamt: shift amount (only used for shift instructions)
     - this field is set to 0 in all but the shift instructions
   - 6 funct: function: combined with opcode, this number exactly specifies the instruction

**Dealing with large immediates**

 - supporse we want: `addiu $t0,$t0,0xABABCDCD`, translates into
   - `lui  $at,0xABAB` load upper immediate: moves 16-bit number into upper half of `reg` and zeros the lower half
   - `ori  $at,$at,0XCDCD` or immediate
   - `addu $t0,$t0,$at` only the assembler gets to use `$at`


**compilation process**

 - `.c` -> `cpp` -> `.i` -> `compiler` -> `.s` -> `assembler` -> `.o` (object code files) -> `linker` -> `a.out` -> `loader` -> memory
 - compiler
   - input: `foo.c`
   - output: `foo.s` may contain pseudoinstructions
 - assembler
   - input: `foo.s` Assembly Language Code (MAL)
   - output: `foo.o` object code, information tables (TAL)
   - things to do:
     - replace pseudoinstructions
     - reads and uses directives
     - produce machine language: symbol table + relocation table
     - creates object files
 - linker
   - input: `foo.o` `libc.o` object code files
   - output: `a.out` executable code
   - things to do:
     - step 1: take text segment from each `.o` file, and put them together
     - step 2: take data segment from each `.o` file, put them together and concatenate this onto end of text segments
     - step 3: resolve references (absolute addresses)
 - loader
   - reads executable file's header to determine size of text and data segments
   - creates new address space to hold text and data segments, along with a stack
   - copies instructions and data from executable file into the new address space
   - copies arguments passed to the program onto the stack
   - initialize machine registers
   - jumps to start-up routine that copies program's arguments from stack to registers & sets the PC

Assembler directives: give directions to assemblers, but do not produce machine instructions

 - `.text:` machine code
 - `.data:` static data 
 - `.global sym:`
 - `.asciiz str:`
 - `.word w1...wn:`

Symbol table: list of items in this file that may be used by other files

 - labels:
 - data: anything in the `.data` section

Relocation table: list of items this file needs the address later

 - labels of `j` or `jal`
 - data in the static section

Object file format (Standard format: ELF, executable linker format):

 - object file header: how big other segments are in this file
 - text segment: the machine code
 - data segment: binary representation of the static data in the source file
 - relocation information: identifies lines of code that need to be fixed up later
 - symbol table: list of this file's labels and static data that can be referenced
 - debug information: points from machine code to original c code