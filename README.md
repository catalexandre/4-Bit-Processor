# 4-Bit-Processor
A 4-Bit Processor built in my system hardware university laboratory

## Index
#### [Introduction](#introduction-1)
#### [Integrated circuits components descriptions](#integrated-circuits-components-descriptions-1)
555<br>
74LS164<br>
7420<br>
74LS283<br>
74LS173<br>
ATtiny2313A<br>
7442<br>
7404<br>
7408<br>
7432<br>
#### Operation of the computer
#### Computer specific workings and wiring
Timing signal generator
Data bus
Program counter
Arithmetic unit
Mirror register
Memory
Data registers
Control signal generator

## Introduction
This lab report describes the process of building a 4-bit computer using different integrated circuits such as registers, logic gates, a clock, and more. The different components that make up this computer include a timing signal generator (TSG), a program counter (PC), an arithmetic logic unit (“ALU”), a sum register, data registers, memory address register (MAR), program memory, a decoder, a control signal generator (CSG), and a bus. 

Once constructed, the computer will be able to execute a simple program of sixteen instructions, varying between five different opcodes. The executable commands are to 
Increment register A
Increment register B
Move the contents of register A to register B
Move the contents of register B to register A
No operation
and are executed in the order saved in a preprogrammed ATtiny2313A microcontroller acting as the computer’s memory.

The following sections of the lab report cover everything there is to know about the construction and functioning of the computer in more detail, from schematics to timing diagrams.

![](final_board.png) <br>
Click here for a [video](https://youtube.com/shorts/8P3Bk8ZhHko?si=GYPgo7M3aASAGeQ_) of the functionning computer.

## Integrated circuits components descriptions
