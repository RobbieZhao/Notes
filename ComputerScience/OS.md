Heat wall -> multicore -> parallelism at all levels


Two types of VMs

 - System VM
 - Process VM

What is a kernel?


Stack

 - local variables, call stack
 - grows down: high address to low address
 
heap

 - grows up

Execution sequence

 - fetch instruction at PC
 - decode the instruction
 - execute (using registers)
 - write results to registers/memory
 - update PC


Thread

 - single execution context
   - PC, registers, everything in memory that counts
 - switch between threads
   - save/load PC, SP, and registers (the state of the thread) into/from the memory
 - share the memory
 - multithreading
   - hardware approach

Process

 - address space with one or more threads
 - Process Control Block: state of a process
 - OS contains a data structure containing the PCBs

Process vs Thread

 - process is more like a container
 - thread is the execution unit
 - Think of them as a box and many mices in it

Hardware provides two modes

 - Kernel
 - User mode

Mode transfer

 - syscall
 - interrupt
 - exception

What is interrupt?

 - signal sent from a device or software to the operating system
 - causes OS to stop what it's doing and service the interrupt


Base & Bound

 - OS could change base & bound, the user mode cannot modify it, and cannot access memory outside the B & B
 - doesn't provide 0
   - add in address space translation

operations on a process

 - getpid()
 - fork()
   - creates a copy of process (except the pid)
   - returns twice, once in the parent, once in the child
     - return > 0 parent process
     - return == 0 child process
     - return < 0 error
 - exec: change the program being run by the current process
 - wait: wait for a process to finish and get the returned value
   - argument: a pointer to store the status
   - return pid of the next terminating child
 - signal: send a notification to another process

what is a file descriptor?


what is a socket


What is stored on stack?

 - temporary variables
 - where to return












