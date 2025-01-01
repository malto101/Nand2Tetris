---
layout: default
title: Module 1
parent: Part 1
nav_order: 4
description: "Module 1 of Nand2Tetris."
permalink: /Part1/Module_1
has_children: false
includes:
  - head_custom.html
---

# Nand2Tetris: Module 1 -  Boolean Logic 

Welcome to the first module of my Nand2Tetris journey! In this module, I delved into the foundations of digital logic design by building basic logic gates.  

## Boolean Values

Boolean values are fundamental representation of numbers in computer. We come with two values **1** and **0**.

## Boolean Operation
They deal with **binary values**—`0` (false) and `1` (true)—and define how these values interact using logical operators.
### Key Boolean Operators  
1. **NOT**  

   - Flips the input value.  
   - Truth Table:  

     | Input | Output |  
     |-------|--------|  
     |   0   |    1   |  
     |   1   |    0   |  

2. **AND**  

   - Outputs `1` only if both inputs are `1`.  
   - Truth Table:  

     | Input A | Input B | Output |  
     |---------|---------|--------|  
     |    0    |    0    |   0    |  
     |    0    |    1    |   0    |  
     |    1    |    0    |   0    |  
     |    1    |    1    |   1    |  

3. **OR**  

   - Outputs `1` if at least one input is `1`.  
   - Truth Table:  

     | Input A | Input B | Output |  
     |---------|---------|--------|  
     |    0    |    0    |   0    |  
     |    0    |    1    |   1    |  
     |    1    |    0    |   1    |  
     |    1    |    1    |   1    |  

4. **XOR (Exclusive OR)**  

   - Outputs `1` only if the inputs are different.  
   - Truth Table:  

     | Input A | Input B | Output |  
     |---------|---------|--------|  
     |    0    |    0    |   0    |  
     |    0    |    1    |   1    |  
     |    1    |    0    |   1    |  
     |    1    |    1    |   0    |  

5. **NAND (NOT AND)**  

   - Outputs `0` only if both inputs are `1`.  
   - Truth Table:  

     | Input A | Input B | Output |  
     |---------|---------|--------|  
     |    0    |    0    |   1    |  
     |    0    |    1    |   1    |  
     |    1    |    0    |   1    |  
     |    1    |    1    |   0    |  

6. **NOR (NOT OR)**  

   - Outputs `1` only if both inputs are `0`.  
   - Truth Table:  

     | Input A | Input B | Output |
     |---------|---------|--------|
     |    0    |    0    |   1    |
     |    0    |    1    |   0    |
     |    1    |    0    |   0    |
     |    1    |    1    |   0    |


## Boolean Identities: The Basics  
Boolean identities are fundamental properties of logical operations that remain true regardless of the inputs.  

### 1. **Identity Laws**  
- **AND Identity:** `A AND 1 = A`  
  - The value of `A` is unchanged when ANDed with `1`.  
- **OR Identity:** `A OR 0 = A`  
  - The value of `A` is unchanged when ORed with `0`.  

### 2. **Null Laws**  
- **AND Null:** `A AND 0 = 0`  
  - Anything ANDed with `0` is always `0`.  
- **OR Null:** `A OR 1 = 1`  
  - Anything ORed with `1` is always `1`.  

### 3. **Idempotent Laws**  
- **AND Idempotent:** `A AND A = A`  
- **OR Idempotent:** `A OR A = A`  
  - Repeating the same operation has no additional effect.  

### 4. **Complement Laws**  
- **AND Complement:** `A AND NOT A = 0`  
- **OR Complement:** `A OR NOT A = 1`  
  - A variable and its complement always cancel each other out.  

---

## Boolean Laws: Making Logic Simpler  
Boolean laws extend identities by introducing equivalences that help reduce or transform logical expressions.  

### 1. **Commutative Laws**  
- `A AND B = B AND A`  
- `A OR B = B OR A`  
  - The order of operations doesn’t matter.  

### 2. **Associative Laws**  
- `(A AND B) AND C = A AND (B AND C)`  
- `(A OR B) OR C = A OR (B OR C)`  
  - Grouping of operations doesn’t matter.  

### 3. **Distributive Laws**  
- `A AND (B OR C) = (A AND B) OR (A AND C)`  
- `A OR (B AND C) = (A OR B) AND (A OR C)`  
  - Operations can be distributed across other operations.  

### 4. **Absorption Laws**  
- `A OR (A AND B) = A`  
- `A AND (A OR B) = A`  
  - Extra terms can be "absorbed" without changing the logic.  

### 5. **De Morgan’s Laws**  
De Morgan's laws are **extremely important** in digital logic and circuit design:  
- `NOT (A AND B) = (NOT A) OR (NOT B)`  
- `NOT (A OR B) = (NOT A) AND (NOT B)`  

## Simplifying Boolean expression

Most often, our usage is going to be much complicated then simple gate usage, which is why we use various methods to simplify a boolean expression.

The method we use **Constructing Disjunctive Normal Form (DNF)** to convert a boolean truth table to a boolean function.

In digital logic, **Disjunctive Normal Form (DNF)** is a method of expressing Boolean functions as a sum (OR) of product terms (ANDs of literals). In this post, we’ll use the truth table of a **2-to-1 Multiplexer (MUX)** to construct the DNF step-by-step.  

### Truth Table of a 2-to-1 MUX  

2:1 Mux

| S | I₀ | I₁ | F  |  
|---|----|----|----|  
| 0 | 0  | 0  |  0 |  
| 0 | 0  | 1  |  0 |  
| 0 | 1  | 0  |  1 |  
| 0 | 1  | 1  |  1 |  
| 1 | 0  | 0  |  0 |  
| 1 | 0  | 1  |  1 |  
| 1 | 1  | 0  |  0 |  
| 1 | 1  | 1  |  1 |  

The output \( F \) depends on \( S \), \( I₀ \), and \( I₁ \). Our goal is to construct the **DNF** for \( F \).  

---

### Steps to Construct the DNF  

#### Step 1: Identify Rows Where the Output Is 1  

From the truth table, focus on the rows where \( F = 1 \).  

| S | I₀ | I₁ | F  |  
|---|----|----|----|  
| 0 | 1  | 0  |  1 |  
| 0 | 1  | 1  |  1 |  
| 1 | 0  | 1  |  1 |  
| 1 | 1  | 1  |  1 |  

#### Step 2: Write the Minterms  

From the truth table, identify the rows where \( F = 1 \). For each such row, write the corresponding minterm:

1. **Row 3:** S = 0, I₀ = 1, I₁ = 0  
   Minterm:  !S * I₀ * !I₁

2. **Row 4:** S = 0, I₀ = 1, I₁ = 1  
   Minterm:  !S * I₀ * I₁

3. **Row 6:** S = 1, I₀ = 0, I₁ = 1  
   Minterm:  S * !I₀ * I₁

4. **Row 8:** S = 1, I₀ = 1, I₁ = 1  
   Minterm:  S * I₀ * I₁


#### Step 3: Combine the Minterms  

Combine all the minterms with OR:  
The formula for F is:  
F = (!S * I₀ * !I₁) + (!S * I₀ * I₁) + (S * !I₀ * I₁) + (S * I₀ * I₁)


### Simplification of DNF  

The canonical DNF is often verbose, but we can simplify it:  

#### Factor Out Common Terms

1. **Combine !S * I₀ * !I₁ and !S * I₀ * I₁:**  
   The common terms here are !S and I₀.  
   !S * I₀ * (!I₁ + I₁) = !S * I₀  
   This simplifies because !I₁ + I₁ = 1 (a tautology).

2. **Combine S * !I₀ * I₁ and S * I₀ * I₁:**  
   The common terms here are S and I₁.  
   S * I₁ * (!I₀ + I₀) = S * I₁  
   This simplifies because !I₀ + I₀ = 1 (again, a tautology).


### Final Simplified DNF (Disjunctive Normal Form)

Now we can express the simplified Boolean function as:

F = (!S * I₀) + (S * I₁)