# 1-bit ALU Design, with Functional Analysis and Physical Verification using Cadence provided GPDK090 in Cadence Virtuoso

<p align="justify"> In this project, a <b>1-bit ALU</b> is designed using <i>bottom-up</i> approach, i.e., the fundamental components are designed before and then integrated afterwards to work as a one functional unit. Also, this design is functionally analysed via simulation (both <b>Pre-Layout</b> and <b>Post-Layout</b>) as well as physically verified (via <b>DRC</b>, <b>LVS</b> and <b>RCX</b>). </p>

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
  - [2.7 Arithmetic Logic Unit](#27-Arithmetic-Logic-Unit)
 
- [3. Design Methodology](#3-Design-Methodology)
  - [3.1 Bottom-Up Approach](#31-Bottom-Up-Approach)
  - [3.2 Functional Analysis](#32-Functional-Analysis)
  - [3.3 Layout and Physical Verification](#33-Layout-and-Physical-Verification)
 
- [4. ALU Design Steps](#4-ALU-Design-Steps)
  - [4.1 Logic Gates Design](#41-Logic-Gates-Design)
  - [4.2 Full Adder Design](#42-Full-Adder-Design)
  - [4.3 MUX Design](#43-MUX-Design)
  - [4.4 ALU Design](#44-ALU-Design)
 
- [5. Conclusion](#5-Conclusion)
  
--- 

## 1. Tool and PDK used

### 1.1 Cadence Virtuoso

<p align="center"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQlqRde5Guj48ZQCn00CIVwFYYiYlWdEDDXFQ&s"></p>

[Cadence Virtuoso](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/virtuoso-studio.html) is a system design platform for analog, mixed-signal, and RF designs. It is a commercially used and critically acclaimed EDA tool and not open-source. The Virtuoso version that I use is provided to me through my institute, and is an integration of multiple [Cadence](https://www.cadence.com/en_US/home.html) products such as [Virtuoso Schematic Editor](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-schematic-editor.html), [Virtuoso ADE Suite](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/circuit-design/virtuoso-ade-suite.html) and [Virtuoso Layout Suite](https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/layout-design/virtuoso-layout-suite.html).

## 1.2 GPDK090
**90nm Generic Process Design Kit** (GPDK090)  is a complete design kit based on a fictitious 90nm BiCMOS process. It is provided by [Cadence](https://www.cadence.com/en_US/home.html) for the purpose of designing, simulating and verifying the ICs for research and educational programs. Manual for the same can be accessed here - [gpdk090-manual](https://www.princeton.edu/~nverma/cadenceSetup_6.1.7/gpdk090_v4.4/docs/gpdk090_spec.pdf).

## 2. Fundamental Components

### 2.1 NOT Gate

<p align="center"><img src="https://media.geeksforgeeks.org/wp-content/uploads/20240328125616/NOT-Gate-1024.png" width="400" height="300" /></p>

<p align="justify">In digital circuits, the NOT gate is a basic logic gate having only a single input and a single output. The output of the NOT gate is logic 0 when its input is logic 1 and the output is logic 1 when its input is logic 0. Thus, the NOT gate is used to perform the inversion operation in digital circuits. It complements the input and produces a corresponding output.</p>

### 2.2 AND Gate

<p align="center"><img src="https://media.geeksforgeeks.org/wp-content/uploads/20240403180605/AND-Gate-in-Digital-Electronics-22.png" width="400" height="300" /></p>

<p align="justify">An AND gate is used to perform logical Multiplication of binary input. The Output state of the AND gate will be high(1) if both the input are high(1) ,else the output state will be low(0) if any of the input is low(0).</p> 

The Boolean Expression or logic for the AND gate is the logical multiplication of inputs denoted by a full stop or single dot as: `X = A.B`. 
The value of X will be True when both the inputs will be True.

### 2.3 OR Gate 

<p align="center"><img src="https://media.geeksforgeeks.org/wp-content/uploads/20241014113543355764/2-input-Or-gate.png" width="400" height="300" /></p>

<p align="justify">OR GATE is most widely used digital logic circuit. The output state of OR gate will be high i.e.,(1) if any of the input state is high or 1, else output state will be low i.e., 0. </p> 

The Boolean Expression for the OR gate is the logical addition of inputs denoted by plus sign(+) as: `X= A+B`. The value of X will be high(true) when one of the inputs is set to high (true).

### 2.4 XOR Gate 

<p align="center"><img src="https://media.geeksforgeeks.org/wp-content/uploads/20240328125139/XOR-Gate.png" width="400" height="300" /></p>

<p align="justify">In digital electronics, there is a specially designed logic gate named, XOR gate, which is used in digital circuits to perform modulo sum. It is also referred to as Exclusive OR gate or Ex-OR gate. it is used extensively in arithmetic logic circuits., logic comparators and error detection circuits. The XOR gate can take only two inputs at a time and give an output. The output of the XOR gate is high(1) only when its two inputs are dissimilar i.e., if one of them is low(0) then other one will be high(1). </p> 

Say we have two inputs, A and B and the output is called X, then the Boolean expression of XOR Gate is: `X = A’B + AB’`.

### 2.5 Full Adder

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/1-77.png">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/2-41.jpg">
</div>

Full Adder is the adder that adds three inputs and produces two outputs. The first two inputs are A and B and the third input is an input carry as C-IN. The output carry is designated as C-OUT and the normal output is designated as S which is SUM. The C-OUT is also known as the majority 1’s detector, whose output goes high when more than one input is high. A full adder logic is designed in such a manner that can take eight inputs together to create a byte-wide adder and cascade the carry bit from one adder to another. we use a full adder because when a carry-in bit is available, another 1-bit adder must be used since a 1-bit half-adder does not take a carry-in bit. A 1-bit full adder adds three operands and generates 2-bit results.

Logical Expression for SUM: `SUM = C-IN XOR (A XOR B)`

Logical Expression for C-OUT: `C-OUT = A B + B C-IN + A C-IN`

### 2.6 4x1 Multiplexer

<p align="center"><img src="https://media.geeksforgeeks.org/wp-content/uploads/20240514095002/Untitled-Diagram---2024-05-14T094946432.webp" width="400" height="300" /></p>

A multiplexer is a combinational circuit that has many data inputs and a single output, depending on control or select inputs. For N input lines, log2(N) selection lines are required, or equivalently, for 2<sup>n</sup> input lines, n selection lines are needed. Multiplexers are also known as “N-to-1 selectors,” parallel-to-serial converters, many-to-one circuits, and universal logic circuits. They are mainly used to increase the amount of data that can be sent over a network within a certain amount of time and bandwidth.
The Mux can be of different types based on input, one of them is 4x1 MUX.

The 4×1 Multiplexer which is also known as the 4-to-1 multiplexer. It is a multiplexer that has 4 inputs and a single output. The Output is selected as one of the 4 inputs which is based on the selection inputs. The number of the Selection lines will depend on the number of the input which is determined by the equation log<sub>2</sub>n, In 4×1 Mux the selection lines can be determined as log<sub>2</sub>4 = 2, so two selections are needed.
In the Given Block Diagram I0, I1, I2, and I3 are the 4 inputs and Y is the Single output which is based on Select lines S0 and S1.

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/1-78.png">
  <img src="https://media.geeksforgeeks.org/wp-content/uploads/2-42.jpg">
</div>

The output of the multiplexer is determined by the binary value of the selection lines:
- When S1S0=00, the input I0 is selected.
- When S1S0=01, the input I1 is selected.
- When S1S0=10, the input I2 is selected.
- When S1S0=11, the input I3 is selected.

### 2.7 Arithmetic Logic Unit

<p align="justify">ALU is a digital circuit that provides arithmetic and logic operations. It is the fundamental building block of the central processing unit of a computer. A modern central processing unit(CPU) has a very powerful ALU and it is complex in design.</p>

<p align="center"><img src="https://media.cheggcdn.com/media/fe6/fe680b29-8523-4ed0-9aa0-a5acf430b5bb/phpTLJJG1" width="400" height="300" /></p>

<p align="justify">It does arithmetic operations like addition, subtraction,division, multiplication and logical oparations like and, or, xor, nand, nor etc. A simple block diagram of a 4 bit ALU for operations and,or,xor and Add is shown above.</p>

## 3. Design Methodology

### 3.1 Bottom-Up Approach

<p align="justify">The design of ALU in this project follows bottom-up approach, to which given below are the steps followed to bit-by-bit design a 1-bit ALU with logic functions AND, OR, XOR and arithmetic function ADD:</p>

- Design a CMOS Inverter, which will practically work as a NOT Gate. This will be further used in the design to invert the signals.
- Design an AND Gate by realising the Boolean function using CMOS Logic.
- Similarly, design OR and XOR Gate to furthur use them in the ALU.
- Design a Full Adder using the gates realised via CMOS Logic.
- Design a 2x1 MUX using the same gates designed before and correspondingly design a 4x1 MUX.
- Test the functionality of each circuit side-by-side using simulations.
- Also, design the layout and perform Physical Verification steps (DRC, LVS and RCX) for each designed circuit.
- Finally, integrate all the designed components and design a 1-bit ALU. Also, perform functional analysis and physical verification steps.

### 3.2 Functional Analysis

In Functional Analysis or **Simulation** is the process of predicting _how a circuit will behave before it's built_. It's used to evaluate the _performance of a system, compare designs, and identify potential issues_. The tools **model the behavior of circuit elements** at different levels of detail. The level of detail depends on the circuit's intended use and the amount of input data it needs to process. If a very large amount of input data must be processed, hardware approaches such as emulation or rapid prototyping are used. These situations occur when a processor’s operating system must be run against real-world scenarios, such as video processing. Without a hardware-assisted approach, the runtime for these cases can be untenable.

### 3.3 Layout and Physical Verification

**Layout** in VLSI refers to the process of creating the __physical representation of an integrated circuit__ (IC) design. It involves **translating the logical circuit description (schematic) into geometric representations of the various layers** used in semiconductor manufacturing.

Purpose:
 - Translate logical design into a physical representation suitable for manufacturing.
 - Optimize chip area, performance, and power consumption.
 - Ensure manufacturability and reliability of the IC.

Process Flow: (_Also termed as_ **Physical Design Flow**)
 - **Floorplanning:** Arranging major functional blocks
 - **Placement:** Positioning individual cells or components
 - **Routing:** Connecting components with metal layers
 - **Compaction:** Optimizing layout for area efficiency
 - **Verification:** DRC, LVS, RCX/XRC

Commercially, there are various tools available for the Physical Verification of the MOS Circuits like _Cadence PVS, Mentor Graphics Calibre, Synopsys IC Validator, etc._ but the tool I utilized to do so is [Cadence Assura](https://www.cadence.com/en_US/home/tools/digital-design-and-signoff/silicon-signoff/assura-physical-verification.html). All the physical verification steps - _DRC, LVS and RCX_ for the project is done via this tool.

#### Design Rule Checking

Design Rule Checks are nothing but **physical checks of metal width, pitch and spacing requirement** for the different layers which _depend on different technology nodes_. We need to **clean up** the DRC of the design because there is a logical connection of various components, and if they are physically connected, then it will fail the functionality of the chips, and chips won’t be able to perform a specific task.

The layout of a design must be in accordance with a set of **predefined technology rules given by the foundry for manufacturability**. After completion of the layout and its physical connection, an automatic program will check each and every polygon in the design against these design rules and report any violations. This whole process is called **Design Rule Checking (DRC)**. 

There are many design rules at different technology nodes, a few of which are mentioned below:
- Minimum width and spacing for metal
- Minimum width and spacing for via
- Fat wire Via keep out Enclosure
- End of Line spacing
- Minimum area
- Over Max stack level
- Wide metal jog
- Misaligned Via wire
- Different net spacing
- Special notch spacing
- Shorts violation
- Different net Via cut spacing
- Less than min edge length

#### Layout Vs Schematic

Layout Versus Schematic (LVS) checking **compares the extracted netlist from the layout to the original schematic netlist to determine if they match**. The comparison check is considered **clean** if all the devices and nets of the schematic match the devices and the nets of the layout. Optionally, the device properties can also be compared to determine if they match within a certain tolerance. When properties are compared, all the properties must match as well to achieve a clean comparison.

Two main processes make up the LVS flow. The first process in the flow is **extraction**, in which _the layers within the layout database are analyzed and all the devices and nets are extracted_. The second process in the flow is **compare**, in which the _actual comparison of devices and nets occurs_.

The LVS runset contains a series of function calls that control both extraction and netlist comparison.

LVS errors can be classified into two main categories:

1. Extraction Errors
   - Text short and open
   - Device extraction error
   - Missing device terminal
   - Extra device terminal
   - Unused text
   - Duplicate structure placement

2. Compare Errors
   - Unmatched nets in the layout/schematic
   - Unmatched devices in the layout/schematic
   - Property errors
   - Port swap errors

#### RC Extraction

**Parasitic Extraction** provide the information about the _parasitic devices which are not included as a part of original circuit design_. But these parasitic devices **affect the circuit performance** in several ways. There are chances that because of these devices, the circuit stops working or does not meet design specifications.

Effect of Parasitic Devices on Circuit Design:

1. Extra Power Consumption
   - violate the Power specification extra power dissipation can increase local temperature which can effect other parameters

2. Effect the Delay of circuit
   - which can cause of timing violation can impact IR drop

3. Reduce the Noise Margin
   - which can cause logic failure

4. Increase Signal Noise which can
   - change the Logic of the signal (0 to 1) or (1 to 0)
   - logic failure introduce extra/unwanted delay which can impact the timing
   - speed up the signal which again impact the timing

5. Increase IR drop on power supply lines
   - which in turn affects delay

In order to get a good idea of realistic parameters in our design, we run RCX which can **estimate and add** to your design the _parasitic resistances (R), capacitances (C), self inductances (L), and mutual inductances (K)_. We are only interested in RC parasitics, hence, **RC Extraction**.

## 4. ALU Design Steps

### 4.1 Logic Gates Design

#### A. **NOT Gate** (_CMOS Inverter_)
Below are the images that illustrates the schematic as well as the symbol designed for the NOT Gate:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/NOT_Gate/NOT_Schematic.png"  width="400" height="500">
  <img src="/NOT_Gate/NOT_Symbol.png" width="400" height="300">
</div>

Design consists of total four ports, namely **IN**(_Input_), **OUT**(_Output_), **VDD**(_Supply_) and **GND**(_Ground_). At IN equals to _Logic-0_(LOW), pMOS turns **ON** while nMOS will be **OFF** and OUT port starts to charge, thus, OUT equals _Logic-1_(HIGH). Similarly, when IN equals to _Logic-1_(HIGH), nMOS turns **ON** while pMOS will be **OFF**, therefore, OUT is grounded, hence, OUT equals _Logic-0_(LOW).

**W/L** Ratios for the transistors (from GPDK090) used is mentioned below:
| Transistor Used | W/L Ratio |
| --------------- | --------- |
| pmos1v          | 985/180   |
| nmos1v          | 420/180   |

_This same ratio will be continued in the other designs._

After this we have to design a **Layout** for the same design, keeping all the rules in mind to design it without encountering any errors aftwerwards. Below is the image showing the layout design of a NOT Gate/CMOS Inverter:

<img src="/NOT_Gate/NOT_Layout.png" width="400" height="500">

Performing **DRC** and **LVS** verification on the NOT Gate Layout Design:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/NOT_Gate/NOT_DRC.png"  width="400" height="500">
  <img src="/NOT_Gate/NOT_LVS.png" width="400" height="500">
</div>

Design Physical Verification Runs imply that the design is **DRC Clean** and **LVS Match**.
Next Step is to perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as NOT Gate **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/NOT_Gate/NOT_RCX.png"  width="400" height="500">
  <img src="/NOT_Gate/NOT_Extracted_View.png" width="400" height="500">
</div>

Now, we design a **testbench** to simulate the circuit to check its functionality with respect to _change in the input signal w.r.t time_. We need a **DC Source** as a _supply voltage_, a connection to the ground and a **varying pulse** as an _input source_. The designed testbench is as follows:

<img src="/NOT_Gate/NOT_Testbench.png">

| Parameter    | Value | Properties                                                                      |
| ------------ | ----- | ------------------------------------------------------------------------------- |
| VDD (Supply) | 1.8 V | DC Voltage Source                                                               |
| GND (Ground) | 0     | Ground Connection                                                               |
| IN (Input)   | 1.8 V | Pulsating Voltage Source (Period = 50ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |

Then, we perform a simulation on this NOT Gate schematic view to study **Pre-Layout** (_Dashed-Line_) working of the design and also utilize the **Extracted-View** to study **Post-Layout**(_Solid-Line_) working of the design. The simulation waveform  results for the same are shown below:

<img src="/NOT_Gate/NOT_Simulation.png">

_Parasitics_ add a delay element to the working of the design, which can be calculated and is demonstrated below:

<img src="/NOT_Gate/NOT_Delay.png">

Delay at the output between Pre-Layout and Post-Layout signal is = **3.67ps**. Therefore, Parasitics do affect the working of a design based on our transient analysis.

#### B. **AND Gate**
Schematic as well as symbol design for the AND Gate:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/AND_Gate/AND_Schematic.png"  width="400" height="300">
  <img src="/AND_Gate/AND_Symbol.png" width="400" height="300">
</div>

Design consists of total five ports, **A, B**(_Inputs_), **OUT**(_Output_), **VDD**(_Supply_) and **GND**(_Ground_). When A and B equals _Logic-0_(LOW), both pMOS turn **ON** while both nMOS will turn **OFF** and the output is inverted by the NOT gate, therefore, OUT equals _Logic-0_(LOW). Also, when A equals _Logic-0_(LOW) and B equals _Logic-1_(HIGH) , pMOS _PM0_ turns **ON** while pMOS _PM1_ will turn **OFF**, and nMOS _NM0_ turns **OFF** while nMOS NM1 turns **ON**, and similar to the previous case, output is still inverted and we get _Logic-0_(LOW) at OUT. Same is the case for A equals _Logic-1_(HIGH) and B equals _Logic-0_(LOW). Finally, when A and B both equals _Logic-1_(HIGH), both pMOS will be turned **OFF** and both nMOS will be turned **ON** and after inverting the output, we get _Logic-1_(HIGH) at the OUT. Thus, this CMOS Logic circuit works as an AND Gate.

Layout Design for this CMOS AND Logic is:

<img src="/AND_Gate/AND_Layout.png" width="500" height="550">

Performing **DRC** and **LVS** verification runs on the AND Gate Layout Design:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/AND_Gate/AND_DRC.png"  width="400" height="450">
  <img src="/AND_Gate/AND_LVS.png"  width="400" height="450">
</div>

This Layout Design passed both runs and is **DRC Clean** as well as **LVS Match**.
Also, perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as AND Gate **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/AND_Gate/AND_RCX.png"  width="400" height="450">
  <img src="/AND_Gate/AND_Extracted_View.png"  width="400" height="450">
</div>

Below is the **testbench** design to simulate and check the functionality of the circuit. We need a **DC Source** as a _supply voltage_, a connection to the ground and two **varying pulses** as  _input source A and B_. The designed testbench is as follows:

<img src="/AND_Gate/AND_Testbench.png">

| Parameter    | Value | Properties                                                                      |
| ------------ | ----- | ------------------------------------------------------------------------------- |
| VDD (Supply) | 1.8 V | DC Voltage Source                                                               |
| GND (Ground) | 0     | Ground Connection                                                               |
| A (Input1)   | 1.8 V | Pulsating Voltage Source (Period = 30ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| B (Input2)   | 1.8 V | Pulsating Voltage Source (Period = 50ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |

**Pre-Layout** as well as **Post-Layout** Simulation results are shown below:

<img src="/AND_Gate/AND_Simulation.png">

Parasitic Delay between the Pre-Layout and Post-Layout output signal can be calculated and done so below:

<img src="/AND_Gate/AND_Delay.png">

Parasitic Delay comes out to be = **10.0499ps**.

#### C. **OR Gate**
Schematic and symbol design for the OR Gate, is shown in the figure(s) below:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/OR_Gate/OR_Schematic.png"  width="400" height="350">
  <img src="/OR_Gate/OR_Symbol.png" width="400" height="350">
</div>

Design consists of total five ports same as the AND Gate, i.e., **A, B**(_Inputs_), **OUT**(_Output_), **VDD**(_Supply_) and **GND**(_Ground_). When A and B equals _Logic-0_(LOW), both pMOS turn **ON** while both nMOS will turn **OFF** and the output is inverted by the NOT gate, therefore, OUT equals _Logic-0_(LOW). But, when A equals _Logic-0_(LOW) and B equals _Logic-1_(HIGH) , pMOS _PM0_ turns **ON** while pMOS _PM1_ will turn **OFF**, and nMOS _NM0_ turns **OFF** while nMOS NM1 turns **ON**, therefore, output is inverted and we get _Logic-1_(HIGH) at OUT. Same is the case for A equals _Logic-1_(HIGH) and B equals _Logic-0_(LOW). Finally, when A and B both equals _Logic-1_(HIGH), both pMOS will be turned **OFF** and both nMOS will be turned **ON** and after inverting the output, we get _Logic-1_(HIGH) at the OUT. Thus, this CMOS Logic circuit works as an OR Gate.

Layout Design for this CMOS OR Logic is:

<img src="/OR_Gate/OR_Layout.png" width="500" height="550">

Performing **DRC** and **LVS** verification runs on the OR Gate Layout Design:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/OR_Gate/OR_DRC.png"  width="400" height="450">
  <img src="/OR_Gate/OR_LVS.png"  width="400" height="450">
</div>

This Layout Design passed both runs and is **DRC Clean** as well as **LVS Match**.
Also, perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as OR Gate **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/OR_Gate/OR_RCX.png"  width="400" height="450">
  <img src="/OR_Gate/OR_Extracted_View.png"  width="400" height="450">
</div>

Below is the **testbench** design to simulate and check the functionality of the circuit. Similar to the AND Gate, We need a **DC Source** as a _supply voltage_, a connection to the ground and two **varying pulses** as  _input source A and B_. The designed testbench is as follows:

<img src="/OR_Gate/OR_Testbench.png">

| Parameter    | Value | Properties                                                                      |
| ------------ | ----- | ------------------------------------------------------------------------------- |
| VDD (Supply) | 1.8 V | DC Voltage Source                                                               |
| GND (Ground) | 0     | Ground Connection                                                               |
| A (Input1)   | 1.8 V | Pulsating Voltage Source (Period = 30ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| B (Input2)   | 1.8 V | Pulsating Voltage Source (Period = 50ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |

**Pre-Layout** as well as **Post-Layout** Simulation results are shown below:

<img src="/OR_Gate/OR_Simulation.png">

Parasitic Delay between the Pre-Layout and Post-Layout output signal can be calculated and done so below:

<img src="/OR_Gate/OR_Delay.png">

Parasitic Delay comes out to be = **10.87ps**.

#### D. **XOR Gate**
Schematic and symbol design for the XOR Gate, is shown in the figure(s) below:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/XOR_Gate/XOR_Schematic.png"  width="400" height="350">
  <img src="/XOR_Gate/XOR_Symbol.png" width="400" height="350">
</div>

Similar to the previously designed two gates, the total number of ports are five, i.e., **A, B**(_Inputs_), **OUT**(_Output_), **VDD**(_Supply_) and **GND**(_Ground_). When A and B equals _Logic-0_(LOW), both upper pMOS (_PM0 and PM1_) turn **ON** while both lower pMOS (_PM2 and PM3_) will turn **OFF**, on the contrary, both nMOS on the left (_NM0 and NM2_) turn **OFF** while both nMOS on the right (_NM1 and NM3_) turn **ON**, therefore, OUT equals _Logic-0_(LOW). But, when A equals _Logic-0_(LOW) and B equals _Logic-1_(HIGH) , pMOS _PM0_ turns **ON** while pMOS _PM1_ will turn **OFF**, opposite happens for pMOS _PM2_ and _PM3_, while nMOS _NM0_ turns **OFF** but nMOS _NM2_ turns **ON** and opposite happens for nMOS _NM1_ and _NM3_, therefore, we get _Logic-1_(HIGH) at OUT. Same is the case for A equals _Logic-1_(HIGH) and B equals _Logic-0_(LOW). Finally, when A and B both equals _Logic-1_(HIGH), both upper pMOS will be turned **OFF** but lower pMOS will be turned **ON**, whereas, both nMOS on the right will be turned **ON** and the ones on the left will be turned **OFF**, hence, we get _Logic-1_(HIGH) at the OUT. Thus, this CMOS Logic circuit works as an XOR Gate.

Layout Design for this CMOS XOR Logic is:

<img src="/XOR_Gate/XOR_Layout.png" width="500" height="550">

Performing **DRC** and **LVS** verification runs on the XOR Gate Layout Design:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/XOR_Gate/XOR_DRC.png"  width="400" height="450">
  <img src="/XOR_Gate/XOR_LVS.png"  width="400" height="450">
</div>

This Layout Design passed both runs and is **DRC Clean** as well as **LVS Match**.
Also, perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as XOR Gate **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/XOR_Gate/XOR_RCX.png"  width="400" height="450">
  <img src="/XOR_Gate/XOR_Extracted_View.png"  width="400" height="450">
</div>

Below is the **testbench** design to simulate and check the functionality of the circuit. Similar to the previously designed two gates, We need a **DC Source** as a _supply voltage_, a connection to the ground and two **varying pulses** as  _input source A and B_. The designed testbench is as follows:

<img src="/XOR_Gate/XOR_Testbench.png">

| Parameter    | Value | Properties                                                                      |
| ------------ | ----- | ------------------------------------------------------------------------------- |
| VDD (Supply) | 1.8 V | DC Voltage Source                                                               |
| GND (Ground) | 0     | Ground Connection                                                               |
| A (Input1)   | 1.8 V | Pulsating Voltage Source (Period = 30ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| B (Input2)   | 1.8 V | Pulsating Voltage Source (Period = 50ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |

**Pre-Layout** as well as **Post-Layout** Simulation results are shown below:

<img src="/XOR_Gate/XOR_Simulation.png">

Parasitic Delay between the Pre-Layout and Post-Layout output signal can be calculated and shown below:

<img src="/XOR_Gate/XOR_Delay.png">

Parasitic Delay comes out to be = **21.045ps**.

### 4.2 Full Adder Design

We use primitive gates that we designed before to realise the Full Adder logic. Below is the schematic design that utilise the gates designed before as well as symbol for the Full Adder:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/Full_Adder/FA_Schematic.png"  width="450" height="300">
  <img src="/Full_Adder/FA_Symbol.png" width="350" height="300">
</div>

Output of the first XOR Gate is fed to the second one along with input **Cin**, which realise the Boolean expression for **SUM**, which is: `SUM = A xor B xor Cin`.
Whereas, the output of the two AND Gates used is fed to the OR Gate, which realise the expression for the **Cout**, i.e., `Cout = A.B + B.Cin + A.Cin`.

Layout for this Full Adder Design is shown below:

<img src="/Full_Adder/FA_Layout.png" width="500" height="550">

Similar to the previous designs, we perform physical verification checks on this layout, i.e., **DRC** and **LVS**. Below are the run details:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/Full_Adder/FA_DRC.png"  width="400" height="450">
  <img src="/Full_Adder/FA_LVS.png"  width="400" height="450">
</div>

This Layout Design passed both runs and is **DRC Clean** as well as **LVS Match**.
Now, perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as Full Adder **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/Full_Adder/FA_RCX.png"  width="400" height="450">
  <img src="/Full_Adder/FA_Extracted_View.png"  width="400" height="450">
</div>

Below is the **testbench** design to simulate and check the functionality of the circuit. For this design, We need a **DC Source** as a _supply voltage_, a connection to the ground and three **varying pulses** as  _input source A, B and Cin_. The designed testbench is:

<img src="/Full_Adder/FA_Testbench.png">

| Parameter    | Value | Properties                                                                      |
| ------------ | ----- | ------------------------------------------------------------------------------- |
| VDD (Supply) | 1.8 V | DC Voltage Source                                                               |
| GND (Ground) | 0     | Ground Connection                                                               |
| A (Input1)   | 1.8 V | Pulsating Voltage Source (Period = 30ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| B (Input2)   | 1.8 V | Pulsating Voltage Source (Period = 50ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| Cin (Input3) | 1.8 V | Pulsating Voltage Source (Period = 80ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |

**Pre-Layout** as well as **Post-Layout** Simulation results are shown below:

<img src="/Full_Adder/FA_Simulation.png">

Parasitic Delay between the Pre-Layout and Post-Layout output signal (in this case **SUM** and **Cout**) can be calculated and shown below:

For **SUM**:
<img src="/Full_Adder/FA_Sum_Delay.png">

For **Cout**(Carry):
<img src="/Full_Adder/FA_Carry_Delay.png">

Parasitic Delay for output **SUM** comes out to be = **77.88ps** and for **Cout** comes out to be = **71.68ps**.

### 4.3 MUX Design

Similar to the Full Adder Design, We use primitive gates to realise the MUX logic. Below is the schematic design that utilise the gates designed before as well as symbol for the 2x1 MUX:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/MUX_4x1/MUX_2x1/MUX_2x1_Schematic.png"  width="450" height="350">
  <img src="/MUX_4x1/MUX_2x1/MUX_2x1_Symbol.png" width="350" height="350">
</div>

Input **A** and **S** is fed to the first AND Gate, whereas, input **B** and the not of the input **S** is fed to the second AND Gate. Output of the both AND Gates is fed to the OR Gate, which realise the boolean function of a 2x1 MUX, i.e., `OUT = A.S + B.S'`.

Layout for this 2x1 MUX Design is shown below:

<img src="/MUX_4x1/MUX_2x1/MUX_2x1_Layout.png" width="500" height="550">

Performing physical verification checks on this layout, i.e., **DRC** and **LVS**. Below are the run details:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/MUX_4x1/MUX_2x1/MUX_2x1_DRC.png"  width="400" height="450">
  <img src="/MUX_4x1/MUX_2x1/MUX_2x1_LVS.png" width="400" height="450">
</div>

This Layout Design passed both runs and is **DRC Clean** as well as **LVS Match**.
Now, perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as 2x1 MUX **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/MUX_4x1/MUX_2x1/MUX_2x1_RCX.png"  width="400" height="450">
  <img src="/MUX_4x1/MUX_2x1/MUX_2x1_Extracted.png"  width="400" height="450">
</div>

Now, we will employ 2x1 MUX Design to furthur design a 4x1 MUX. The schematic as well as symbol for the same is illustrated below:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/MUX_4x1/MUX_4x1_Schematic.png"  width="450" height="350">
  <img src="/MUX_4x1/MUX_4x1_Symbol.png" width="350" height="350">
</div>

We used three 2x1 MUXes to create a one 4x1 MUX by feeding output of two 2x1 MUXes to the input of third 2x1 MUX. As we got four inputs, therefore _select lines_ are two.

Layout for this 4x1 MUX Design is shown below:

<img src="/MUX_4x1/MUX_4x1_Layout.png" width="500" height="550">

Performing physical verification checks on this layout, i.e., **DRC** and **LVS**. Below are the run details:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/MUX_4x1/MUX_4x1_DRC.png"  width="400" height="450">
  <img src="/MUX_4x1/MUX_4x1_LVS.png" width="400" height="450">
</div>

This Layout Design passed both runs and is **DRC Clean** as well as **LVS Match**.
Now, perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as 4x1 MUX **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/MUX_4x1/MUX_4x1_RCX.png"  width="400" height="450">
  <img src="/MUX_4x1/MUX_4x1_Extracted_View.png"  width="400" height="450">
</div>

The **testbench** is designed to simulate and check the functionality of the circuit. For this design, We need a **DC Source** as a _supply voltage_, a connection to the ground and six **varying pulses** as  _inputs A, B, C, D and select lines S0 and S1_. The designed testbench is shown below:

<img src="/MUX_4x1/MUX_4x1_Testbench.png">

| Parameter    | Value | Properties                                                                      |
| ------------ | ----- | ------------------------------------------------------------------------------- |
| VDD (Supply) | 1.8 V | DC Voltage Source                                                               |
| GND (Ground) | 0     | Ground Connection                                                               |
| A (Input1)   | 1.8 V | Pulsating Voltage Source (Period = 10ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| B (Input2)   | 1.8 V | Pulsating Voltage Source (Period = 20ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| C (Input3)   | 1.8 V | Pulsating Voltage Source (Period = 30ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| D (Input4)   | 1.8 V | Pulsating Voltage Source (Period = 50ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| S0 (Sel1)    | 1.8 V | Pulsating Voltage Source (Period = 100ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns)|
| S1 (Sel2)    | 1.8 V | Pulsating Voltage Source (Period = 200ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns)|

**Post-Layout** Simulation results are shown below (As it would be cumbersome to append Pre-Layout result together):

<img src="/MUX_4x1/MUX_4x1_Simulation.png">

As we can see, when _S0S1_ = **11**, the OUT equals **A**. When _S0S1_ = **01**, OUT equals **B**, whereas, when _S0S1_ = **10**, OUT equals **C**. Finally, when _S0S1_ = **00**, OUT equals D. This satisfies the working of a 4x1 MUX.

### 4.4 ALU Design

To design Arithmetic Logic Unit (ALU), we will utilize all the previous designs, i.e., Logic Gates, Full Adder and 4x1 MUX and integrate them to work as a one functional unit. Figure(s) below illustrate the schematic as well as symbol view for a 1-bit ALU:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/ALU/ALU_Schematic.png"  width="450" height="400">
  <img src="/ALU/ALU_Symbol.png" width="350" height="400">
</div>

Here, input **A** of the ALU will perform AND operation, input **B** will perform OR operation, input **C** will perform XOR operation and input **D** will perform an addition operation.

Layout for this 1-bit ALU is shown below:

<img src="/ALU/ALU_Layout.png" width="500" height="550">

Performing necessary physical verification checks on this layout, i.e., **DRC** and **LVS**. Below are the run details:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/ALU/ALU_DRC.png"  width="400" height="450">
  <img src="/ALU/ALU_LVS.png" width="400" height="450">
</div>

This Layout Design passed both runs and is **DRC Clean** as well as **LVS Match**.
Now, perform **RC Extraction** on the design, to get parasitic extracted view. Below is the **RCX** run details as well as ALU **Extracted View**:

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="/ALU/ALU_RCX.png"  width="400" height="450">
  <img src="/ALU/ALU_Extracted_View.png"  width="400" height="450">
</div>

The **testbench** is designed to simulate and check the functionality of this 1-bit ALU. For this design, We need a **DC Source** as a _supply voltage_, a connection to the ground and five **varying pulses** as  _inputs A, B, Cin and select lines S0 and S1_. The designed testbench is shown below:

<img src="/ALU/ALU_Testbench.png">

| Parameter    | Value | Properties                                                                      |
| ------------ | ----- | ------------------------------------------------------------------------------- |
| VDD (Supply) | 1.8 V | DC Voltage Source                                                               |
| GND (Ground) | 0     | Ground Connection                                                               |
| A (Input1)   | 1.8 V | Pulsating Voltage Source (Period = 30ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| B (Input2)   | 1.8 V | Pulsating Voltage Source (Period = 50ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| Cin (Input3) | 1.8 V | Pulsating Voltage Source (Period = 40ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns) |
| S0 (Sel1)    | 1.8 V | Pulsating Voltage Source (Period = 100ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns)|
| S1 (Sel2)    | 1.8 V | Pulsating Voltage Source (Period = 200ns, t<sub>rise</sub>=t<sub>fall</sub>=1ns)|

**Post-Layout** Simulation results are shown below (ignoring Pre-Layout results to avoid confusion):

<img src="/ALU/ALU_Simulation.png">

As we can see, when _S0S1_ = **11**, ALU performs AND operation, when _S0S1_ = **01**, ALU performs OR operation, when _S0S1_ = **10**, ALU performs XOR operation and when _S0S1_ = **00** ALU performs Addition where output is recieved at the SUM and Cout bit.

After integrating all the components, we can clearly see the functionality of an ALU in action.

## 5. Conclusion

In conclusion, a **1-bit ALU** with basic arithmetic (_Addition_) and logical (_AND, OR and XOR_) operations was implemented successfully using Cadence Virtuoso. All the design rules (_DRC, LVS and RCX_) for implementing the design are satisfied. The design is optimized following the _stick diagram_ using **Euler's path** and designed using the _minimum possible number of transistors_ in order to _reduce the power consumption and to increase the performance_.
