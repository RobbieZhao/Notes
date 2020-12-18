# [CS/ECE 3810 Computer Organization](http://www.cs.utah.edu/~rajeev/cs3810/)

University of Utah, Spring 2020

**Moore's law**

 - The number of transistors in a dense integrated circuit (IC) doubles about every two years.
 - [18 months or 2 years?](https://www.quora.com/Have-there-been-studies-as-to-why-18-months-for-Moores-law)

**The slow down in microprocessor performance**

From 1986-2003, the performance of microprocessor has been growing at around 52% annually, then from 2003 to 2012, it has been growing at around 22%. Why?

 - Power wall. When dynamic power is above certain level, we need better cooling techniques.
 - Most of the low hanging fruit has been picked: The easy ways to improve performance have been employed.

Dynamic power: Activity × Capacity × Voltage <sup>2</sup> × frequency

 - Activity: number of transistors on the chip that are switching on and off.
 - Capacity of each of the transistors
 - Voltage that the transistors are operating at
 - Frequency: in a second how many times the transistors are switching on and off

Before 2003, Activity up, capacity down, voltage down, frequency up.

Since 2003, voltage and frequency has been somewhat constant. Activity and capacity has cancelled. So the power consumption has been stagnant.

**How to measure performance?**

Performace metrics:

 - response time: time elapsed between start and end of a program
   - performance = 1 / execution time
   - execution time = response time = wall clock time
   - this includes time to execute the workload as well as time spent by the operating system coordinating various events
 - throughput: amount of work done in a fixed time

System X executes a program in 10s, system Y executes the same program in 15 seconds.

 - System X is 1.5 times faster than system Y
 - The speedup of X over Y is 1.5
 - The performance improvement of X over Y is 50%

**Clocks and cycles**

A processor consists of different blocks: adder, ... They are controlled by a clock, which is a voltage going up and down. When the voltage is up, the units look at the inputs and doing computations. Every rising edge is the start of a new cycle.

If an adder takes 800 ps to do one operation. Next cycle should arrive after 800 ps. That's 1 / 800 ps = 1.25 * 10<sup>9</sup>, which is 1.25 GHz. Of course we are taking the slowest operation in consideration.

CPI: cycle per instruction

CPU execution time = CPU clock cycles × clock cycle time

clock cycle time = 1 / clock speed






