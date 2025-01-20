# 1-bit ALU Design, with Functional Analysis and Physical Verification using Cadence provided GPDK090 in Cadence Virtuoso

In this project, a **1-bit ALU** is designed using _bottom-up_ approach, i.e., the fundamental components are designed before and then integrated afterwards to work as a one functional unit. Also, this design is functionally analysed via simulation (both **Pre-Layout** and **Post-Layout**) as well as physically verified (via **DRC**, **LVS** and **RCX**).

## CONTENT

- [1. Tool and PDK used](#1-Tool-and-PDK-used)
  - [1.1 Cadence Virtuoso](#11-Cadence-Virtuoso)
  - [1.2 GPDK090](#12-GPDK090)
 
- [2. Fundamental Components](#2-Fundamental-Components)
  - [2.1 NOT Gate](#21-NOT-Gate)
  - [2.2 AND Gate](#22-AND-Gate)
  - [2.3 OR Gate](#23-OR-Gate)
  - [2.4 XOR Gate](#24-XOR-Gate)
  - [2.5 Full Adder](#25-Full-Adder)
  - [2.6 4x1 Multiplexer](#26-4x1-Multiplexer)
 

## 1. Tool and PDK used

### 1.1 Cadence Virtuoso
![image](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQlqRde5Guj48ZQCn00CIVwFYYiYlWdEDDXFQ&s)

[Cadence Virtuoso](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/virtuoso-studio.html) is a system design platform for analog, mixed-signal, and RF designs. It is a commercially used and critically acclaimed EDA tool and not open-source. The Virtuoso version that I use is provided to me through my institute, and is an integration of multiple [Cadence](https://www.cadence.com/en_US/home.html) products such as [Virtuoso Schematic Editor](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-schematic-editor.html), [Virtuoso ADE Suite](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-ade-suite.html) and [Virtuoso Layout Suite](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/layout-design/virtuoso-layout-suite.html).

## 1.2 GPDK090
**90nm Generic Process Design Kit** (GPDK090)  is a complete design kit based on a fictitious 90nm BiCMOS process. It is provided by [Cadence](https://www.cadence.com/en_US/home.html) for the purpose of designing, simulating and verifying the ICs for research and educational programs. Manual for the same can be accessed here - [gpdk090-manual](https://www.princeton.edu/~nverma/cadenceSetup_6.1.7/gpdk090_v4.4/docs/gpdk090_spec.pdf).

## 2. Fundamental Components

### 2.1 NOT Gate

![Not_Gate](https://media.geeksforgeeks.org/wp-content/uploads/20240328125616/NOT-Gate-1024.png)

In digital circuits, the NOT gate is a basic logic gate having only a single input and a single output. The output of the NOT gate is logic 0 when its input is logic 1 and the output is logic 1 when its input is logic 0. Thus, the NOT gate is used to perform the inversion operation in digital circuits. It complements the input and produces a corresponding output.

### 2.2 AND Gate

![AND_Gate](https://media.geeksforgeeks.org/wp-content/uploads/20240403180605/AND-Gate-in-Digital-Electronics-22.png)

An AND gate is used to perform logical Multiplication of binary input. The Output state of the AND gate will be high(1) if both the input are high(1) ,else the output state will be low(0) if any of the input is low(0). The Boolean Expression or logic for the AND gate is the logical multiplication of inputs denoted by a full stop or single dot as: `A.B=X`. 
The value of X will be True when both the inputs will be True.

### 2.3 OR Gate 

![OR_Gate](https://media.geeksforgeeks.org/wp-content/uploads/20241014113543355764/2-input-Or-gate.png)

OR GATE is most widely used digital logic circuit. The output state of OR gate will be high i.e.,(1) if any of the input state is high or 1, else output state will be low i.e., 0. The Boolean Expression for the OR gate is the logical addition of inputs denoted by plus sign(+) as: `X= A+B`. The value of X will be high(true) when one of the inputs is set to high (true).

### 2.4 XOR Gate 

![XOR_Gate](https://media.geeksforgeeks.org/wp-content/uploads/20240328125139/XOR-Gate.png)

In digital electronics, there is a specially designed logic gate named, XOR gate, which is used in digital circuits to perform modulo sum. It is also referred to as Exclusive OR gate or Ex-OR gate. it is used extensively in arithmetic logic circuits., logic comparators and error detection circuits. The XOR gate can take only two inputs at a time and give an output. The output of the XOR gate is high(1) only when its two inputs are dissimilar i.e., if one of them is low(0) then other one will be high(1). Say we have two inputs, A and B and the output is called X, then the Boolean expression of XOR Gate is: `X = A’B + AB’`.

### 2.5 Full Adder

![Full_Adder_Sym](https://media.geeksforgeeks.org/wp-content/uploads/1-77.png)
![Full_Adder_TT](https://media.geeksforgeeks.org/wp-content/uploads/2-41.jpg)

Full Adder is the adder that adds three inputs and produces two outputs. The first two inputs are A and B and the third input is an input carry as C-IN. The output carry is designated as C-OUT and the normal output is designated as S which is SUM. The C-OUT is also known as the majority 1’s detector, whose output goes high when more than one input is high. A full adder logic is designed in such a manner that can take eight inputs together to create a byte-wide adder and cascade the carry bit from one adder to another. we use a full adder because when a carry-in bit is available, another 1-bit adder must be used since a 1-bit half-adder does not take a carry-in bit. A 1-bit full adder adds three operands and generates 2-bit results.

Logical Expression for SUM: `SUM = C-IN XOR (A XOR B)`

Logical Expression for C-OUT: `C-OUT = A B + B C-IN + A C-IN`

### 2.6 4x1 Multiplexer

![Multiplexer](https://media.geeksforgeeks.org/wp-content/uploads/20240514095002/Untitled-Diagram---2024-05-14T094946432.webp)

A multiplexer is a combinational circuit that has many data inputs and a single output, depending on control or select inputs. For N input lines, log2(N) selection lines are required, or equivalently, for 2<sup>n</sup> input lines, n selection lines are needed. Multiplexers are also known as “N-to-1 selectors,” parallel-to-serial converters, many-to-one circuits, and universal logic circuits. They are mainly used to increase the amount of data that can be sent over a network within a certain amount of time and bandwidth.
The Mux can be of different types based on input, one of them is 4x1 MUX.

The 4×1 Multiplexer which is also known as the 4-to-1 multiplexer. It is a multiplexer that has 4 inputs and a single output. The Output is selected as one of the 4 inputs which is based on the selection inputs. The number of the Selection lines will depend on the number of the input which is determined by the equation log<sub>2</sub>n, In 4×1 Mux the selection lines can be determined as log<sub>2</sub>4 = 2, so two selections are needed.
In the Given Block Diagram I0, I1, I2, and I3 are the 4 inputs and Y is the Single output which is based on Select lines S0 and S1.

![4to1MUX](https://media.geeksforgeeks.org/wp-content/uploads/1-78.png)
![4to1MUX_TT](https://media.geeksforgeeks.org/wp-content/uploads/2-42.jpg)

The output of the multiplexer is determined by the binary value of the selection lines:
- When S1S0=00, the input I0 is selected.
- When S1S0=01, the input I1 is selected.
- When S1S0=10, the input I2 is selected.
- When S1S0=11, the input I3 is selected.
