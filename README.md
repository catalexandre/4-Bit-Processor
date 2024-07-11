# 4-Bit-Processor
A 4-Bit Processor built in my system hardware university laboratory

## Index
#### [Introduction](#introduction-1)
#### [Integrated circuits components descriptions](#integrated-circuits-components-descriptions-1)
- [555](#555-timer)<br>
- [74LS164](#74ls164-sipo-shift-register)<br>
- [7420](#7420-nand-gate)<br>
- [74LS283](#74ls283-4-bit-adder)<br>
- [74LS173](#74ls173-4-bit-register)<br>
- [ATtiny2313A](#attiny2313a)<br>
- [7442](#7442-decoder)<br>
- [7404](#7404-not-----gate)<br>
- [7408](#7408-and----gate)<br>
- [7432](#7432-or----gate)<br>
#### Computer specific workings and wiring
- [Timing signal generator](#Timing-Signal-Generator)
- Data bus
- Program counter
- Arithmetic unit
- Mirror register
- Memory
- Data registers
- Control signal generator

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

Shown in the following figure is a picture of the finished computer:
![](final_board.png) <br>
Click here for a [video](https://youtube.com/shorts/8P3Bk8ZhHko?si=GYPgo7M3aASAGeQ_) of the functionning computer.

## Integrated circuits components descriptions
This section will introduce every integrated circuit used in this lab. Specific wiring between ICs will be discussed in later sections, differences in wiring and functionality for the same IC will also be discussed in other sections, this is only an overview and an explanation for important pins.

NOTE: Please refer to any official documentation for the pin-out diagram of each component  

Below is every component in the computer and the integrated circuits they are composed of

#### Timing signal generator (TSG)
555 Timer - clock<br>
74LS164 SIPO shift register - timing signal generator<br>
7420 NAND gate - input for the timing signal generator
#### Arithmetic unit (“ALU”) and program counter (PC)
74LS283 4-bit adder - pseudo ALU (can only add)<br>
74LS173 4-bit register - program counter<br>
74LS173 4-bit register - sum register<br>
74LS173 4-bit register - mirror register<br>
7404 NOT gate - invert clock signals
#### Data registers and memory address register (MAR)
74LS173 4-bit register - data register A<br>
74LS173 4-bit register - data register B<br>
74LS173 4-bit register - memory address register
#### Program memory (ROM)
ATtiny2313A - read-only memory block<br>
7442 decoder
#### Control signal generator
7408 AND gate<br>
7432 OR gate

### Integrated Circuis

In general, pins with label VCC should be connected to VCC, and GND linked to ground.
In this lab, LEDs are used to see the outputs. To connect an LED, link the output on the side with words (anode), then on the blank side (cathode) link a grounded bussed resistor pack.
 
#### 555 Timer
This IC is used as the clock of the computer.
Pin 4 is a reset pin, it gets triggered when the input is a “logic 0”. Therefore, it must be wired to VCC/logic 1 to prevent it from constantly resetting
Pin 3 is the clock output
Two resistor and two capacitors are also needed to wire this IC functionally

#### 74LS164 SIPO shift register
This IC creates a timing signal since it shifts its content by one output every clock cycle. Input signals are obtained from the NAND gate.
Pin 9 clears the register, it triggers when getting logic 0 so wire it to VCC to prevent that
Pin 1 & 2 are the input pins, it is a AND logic gate and should be tied together
Pin 3-6 and 10-13 are the output pins, with QA as T0, QH is T7, and all the in-betweens

#### 7420 NAND gate
This NAND gate takes 4 inputs, ANDs them and inverts the result. It takes 4 inputs from the 74LS164 and returns 74LS164’s inputs
Pin 3 and pin 11 have no particular function
The inputs from the 74LS164 should be taken from pins 4(QB), 6(QD), 11(QF), 12(QG)

#### 74LS283 4-bit adder
This component is used to increment the number inputted from the bus
Pins 5(X0), 3(X1), 14(X2), 12(X3) should be linked to the bus to get the input
Pins 6, 2, 15, 11 (Y0 to Y3) should be grounded for the second input to be 0
Pin 7 (carry in) should be wired to VCC to obtain the +1 increment
Pins 4, 1, 13, 10 (SUM0 to SUM3) will be linked to the sum register (and not directly onto the bus to prevent bus conflict)
The order of the bits matter

#### 74LS173 4-bit register 
This component can save 4 bits of data input and output it when needed
Pin 15 clears the register, it triggers on active high (logic 1) so ground it to prevent that
Pin 7 is the clock, this clock is positive edge triggered (when clock goes from 0 to 1). However, the computer being built is negative edge triggered, so clock inputs have to be inverted in order for these components to follow the timing
Pin 9 and 10 are the write-enable inputs. They are always grounded (logic 0) so that the register can save new data
Pin 1 and 2 are the output-enable pins, the register can only output when they both have logic 0, so they must be tied together

#### ATtiny2313A
This component has 16 instructions precoded and serves as the memory of the computer. The memory cannot be reprogrammed, meaning its a ROM (read-only memory)
Pin 1 is the reset pin and must be linked to VCC with a 47kΩ resistor
Pin 2, 3, 6, 7 (PD0 to PD3) are the address pins, the inputs are obtained from the MAR
Pin 12, 13, 14, 15 (PB0 to PB3) are the output pins of information encoded at the address

#### 7442 decoder
This component translate binary numbers into active low decimal output
Pin 15, 14, 13, 12 (I0 to I3) are the input pins, from the ATtiny2313A
Pin 1, 2, 3, 4, 5, 6, 7, 9, 10, 11 (Y0 to Y9) are the output pins, although for the purposes of the lab only the first 5 are needed

#### 7404 NOT ( - ) gate
Contains 6 sets of inverting logic gates, one input for one output

#### 7408 AND ( & ) gate
Contains 4 sets of AND logic gates, two inputs for one output

#### 7432 OR ( || ) gate
Contains 4 sets of OR logic gates, two inputs for one output

Shown in the following figure is a picture showing what each integrated circuit is in the computer:
![](board_components.jpg)

## Computer Specific Workings and Wiring

This section is mostly about how each part of the computer works and communicates between each component, along with more wiring connections.

The following figure is a diagram of every component in the computer which will help in understanding the processors functionning:
![](computer_diagram.png)

#### Timing Signal Generator
Timing Signal Generator
The timing signal generator is the first important component of the computer which dictates when every piece of hardware can communicate with each other, making the computer's components work in perfect synchronization. It uses a 555 timing circuit to generate a pulsating clock with a frequency of around 3.25Hz, meaning that it completes a cycle of going from a logical zero, or low voltage, to a high voltage logical one and back to low voltage 3.25 times per second. Moreover, the ratio representing the amount of time for which the logical 1 is held - compared to the logical zero during a clock cycle - is known as the duty cycle.

The 555 clock is wired with 22kΩ (R1) and 56kΩ (R2) resistors, as well as 3.3nF (C2) and 10nF (C1) capacitors, allowing the frequency and duty cycle to be calculated using the below formulas.

![](equations.png)

These calculations reveal that the frequency of the 555 timing circuit is 3.25Hz and that the duty cycle is of 58%, meaning that the “logical one” is held for 58 percent of the whole duration of the clock cycle.

This clock cycle is then fed into pin 8 of a 74LS164 shift register, as seen in figure 1, which shifts all values within its eight internal flip flops when a positive edge is detected in the clock signal. This means that when the clock signal goes from zero to a one, the value from the first flip flop is shifted into the second, and so on. The value shifted in the first flip flop is determined by the ANDing the shift register’s A and B pins, which in this computer’s case are connected to the output of a four input 7420 NAND gate whose inputs are the values of the second, fourth, sixth and seventh flip flop of the shift register, or pins QB, QD, QF, and QG. This has the effect of creating a feedback which will shift two consecutive zeros into the shift register filled with ones, making zeros “float” within a “sea of ones”. Connecting the shift register’s outputs to an LED pack helps visualize this phenomenon consisting of two turned off leds being moved to the end of the LED pack, returning at the other end once they disappear, as seen in table & diagram 1.

The following table shows the inputs and outputs of the timing signal generator:
![](TSG_table.png)

![](TSG_timing_diagram.png)
