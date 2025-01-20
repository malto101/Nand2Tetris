---
layout: default
title: Module 3
parent: Part 1
nav_order: 4
description: "Module 3 of Nand2Tetris."
permalink: /Part1/Module_3
has_children: false
includes:
  - head_custom.html
---

# Nand2Tetris: Module 1 -  Memory

Memory aka remembering something is inherently time-dependent. We use sequential logic to deal with this. We delve in the high level understanding of these memory.

Before we dive into building a simple RAM model, it’s important to first understand the fundamental difference between these circuit types, as it forms the foundation for much of the work in digital electronics, especially in systems like Nand2Tetris.

Combinational circuits are digital circuits where the output is solely determined by the current inputs. They do not have any memory or feedback loops.

while, sequential circuits have memory. This means that their outputs depend not only on the current inputs but also on the sequence of past inputs. In other words, sequential circuits “remember” previous states and use this memory to influence future outputs. This is often achieved through elements like flip-flops or latches, which store the state of the circuit.

## Backgroud

1. **Clock:** The passage of time is reperesented by a master clock that delivers a continous train of alternating signal of 0's and 1's. 

2. **Flip-Flops:** It is the most elementary element in the computer. within this course. i will be mainly using the Data Flip-flips(DFF) which consist of:
    
    - input: single bit data[t-1]
    - input: clock (represented by a triangle within the unit)
    - output: single bit data[t]
    
---
    
**NOTE:**
- **`↑`: Indicates a rising edge of the clock signal.**
- **`X`: "Don't care" — the input is irrelevant when there is no clock edge.**

### Flip-Flops Truth Table

| Clock | D | Q(t+1) | Description                            |
|:-----:|:-:|:------:|:--------------------------------------:|
| ↑     | 0 | 0      | On rising edge, output follows D input |
| ↑     | 1 | 1      | On rising edge, output follows D input |
| 0     | X | Q(t)   | Output holds previous value            |
| 1     | X | Q(t)   | Output holds previous value            |

## Registers: 

It is a storage device that can "store", a value over time. 

### Registers Truth Table

| Clock | Load | D | Q(t+1) | Description                  |
|:-----:|:----:|:-:|:------:|:----------------------------:|
| ↑     | 1    | 0 | 0      | Load new value from D        |
| ↑     | 1    | 1 | 1      | Load new value from D        |
| ↑     | 0    | X | Q(t)   | Maintain current value       |
| 0     | X    | X | Q(t)   | Hold state (level-triggered) |

**NOTE: The main difference between a DFF and a  register is that, a DFF can only output its previous input but a register can remember over long periods of time as long as it is powered.**

## (Random Access Memory)RAM: 

If we combine eight 1-register-> making it a 8-bit register. and then add have eight 8-bit register with their own address. we have created a RAM. A RAM can store data to the registers within in by passing the input data, load bit and the address of the specfic register to where it is should be stored.

### (Random Access Memory)RAM Truth Table

| A2  | A1  | A0  | Load | Data In  | Data Out       | Operation        |
|:---:|:---:|:---:|:----:|:--------:|:--------------:|:----------------:|
| 0   | 0   | 0   | 0    | X        | Word 0 (D[7:0])| Read Word 0      |
| 0   | 0   | 0   | 1    | D[7:0]   | X              | Write Word 0     |
| 0   | 0   | 1   | 0    | X        | Word 1 (D[7:0])| Read Word 1      |
| 0   | 0   | 1   | 1    | D[7:0]   | X              | Write Word 1     |
| 0   | 1   | 0   | 0    | X        | Word 2 (D[7:0])| Read Word 2      |
| 0   | 1   | 0   | 1    | D[7:0]   | X              | Write Word 2     |
| 0   | 1   | 1   | 0    | X        | Word 3 (D[7:0])| Read Word 3      |
| 0   | 1   | 1   | 1    | D[7:0]   | X              | Write Word 3     |
| 1   | 0   | 0   | 0    | X        | Word 4 (D[7:0])| Read Word 4      |
| 1   | 0   | 0   | 1    | D[7:0]   | X              | Write Word 4     |
| 1   | 0   | 1   | 0    | X        | Word 5 (D[7:0])| Read Word 5      |
| 1   | 0   | 1   | 1    | D[7:0]   | X              | Write Word 5     |
| 1   | 1   | 0   | 0    | X        | Word 6 (D[7:0])| Read Word 6      |
| 1   | 1   | 0   | 1    | D[7:0]   | X              | Write Word 6     |
| 1   | 1   | 1   | 0    | X        | Word 7 (D[7:0])| Read Word 7      |
| 1   | 1   | 1   | 1    | D[7:0]   | X              | Write Word 7     |

**NOTE: In the similar manner, we had done by stacking register, we can stack RAM to increase the storage.**

## Counter:

A counter is a sequential chip whose state is an integer number that
increments every time unit. 

A counter comes with 3 control bits to manipulate the value:

1. Reset: It is used to initialize or reset the circuit to Zero.
2. Inc: short for increment, it is used to increment the value currently stored in counter by 1.
3. load: similar to previous chip, This bit is used to load the new value to the program counter

### Counter Truth Table

| Reset | Inc | Load | In  | Q1 (MSB) | Q0 (LSB) | Next State |
|:-----:|:---:|:----:|:---:|:--------:|:--------:|:----------:|
|   0   |  0  |   0  |  x  |    0     |    0     |     00     |
|   1   |  0  |   0  |  x  |    0     |    0     |     00     |
|   0   |  1  |   0  |  x  |    0     |    1     |     01     |
|   0   |  1  |   0  |  x  |    1     |    0     |     10     |
|   0   |  1  |   0  |  x  |    1     |    1     |     11     |
|   0   |  0  |   1  |  01 |    0     |    1     |     01     |
|   1   |  0  |   0  |  x  |    0     |    0     |     00     |
|  ...  | ... |  ... | ... |   ...    |   ...    |    ....    |

