# Binary Systems
---
## Definition

Binary systems are a way of representing numbers using only two symbols: **0** and **1**.

---

## Advantages of Binary Systems

### 1. Simplicity in Hardware

Only two states (0 and 1) are needed, which match OFF and ON electrical signals.

**Example:**  
A switch in a circuit can easily represent 0 (OFF) and 1 (ON).

---

### 2. Reliability / Noise Immunity

With only two states, circuits are less sensitive to small voltage fluctuations.

**Example:**  
A signal of 4.9V is clearly interpreted as 1, while 0.1V is 0, reducing errors.

---

### 3. Ease of Logical Operations

Boolean logic maps naturally to binary numbers.

**Example:**  
AND, OR, NOT operations can be implemented directly in hardware.

---

### 4. Compact Representation in Digital Electronics

Large amounts of data can be stored using only bits.

**Example:**  
An 8-bit byte can store 256 different values (0–255).

---

### 5. Universality in Computing

Binary can represent any number, character, or instruction.

**Example:**  
ASCII codes for letters use 7 or 8 bits per character.

---

## Disadvantages of Binary Systems

### 1. Inefficient for Human Reading

Binary numbers are long and hard to interpret compared to decimal.

**Example:**  
Decimal 255 → Binary 11111111 (harder for humans to read).

---

### 2. More Bits Needed for Large Numbers

Representing large numbers requires many bits.

**Example:**  
Decimal 1023 → Binary 1111111111 (10 bits).

---

### 3. Memory and Bandwidth Overhead

Sometimes storing in binary may take more memory than using other numeral systems like decimal-coded formats.

---

### 4. Complex Arithmetic for Humans

Performing calculations in binary is harder manually.

**Example:**  
Adding 101101 + 11011 requires careful column-wise addition, unlike simple decimal addition.

---

## Binary Number Code Categories — Summary Table

| Category | Codes Included | Purpose / Notes |
|--------|----------------|-----------------|
| **Pure Binary Codes** | Natural Binary, Straight Binary | Standard base-2 representation without weighting tricks. |
| **Weighted Codes** | BCD (8421), Excess-3, 5211, 2421 | Each digit has fixed positional weights; used for decimal digit encoding. |
| **Non-Weighted Codes** | Gray Code, Johnson Code, Fibonacci Code | Codes without fixed positional weights; used in counters and error reduction. |
| **Alphanumeric Codes** | ASCII, Extended ASCII, Unicode | Encodes letters, digits, punctuation, and control characters. |
| **Error-Detecting Codes** | Parity (even/odd), VRC, LRC | Detect transmission/storage errors. |
| **Error-Detecting & Correcting Codes** | Hamming Code, CRC, Reed–Solomon | Detect and correct errors; used in memory, storage, networking. |
| **Signed Number Representations** | Sign-Magnitude, 1’s Complement, 2’s Complement, Excess-128 | Binary formats for positive/negative numbers. |
| **Special Digital Logic Codes** | Gray, Biquinary, Ring Counter Codes | Used in counters, rotary encoders, and state machine design. |

---

<p align="center">
  <img src="../media/flow.jpg" style="width: 100%; max-width: 800px; height: auto;">
  <br>
  <em>Figure 1: Classification of Binary Number Codes</em>
</p>