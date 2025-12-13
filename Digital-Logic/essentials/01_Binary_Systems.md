# Binary Systems

---

## Definition

Binary systems represent information using only two symbols: **0** and **1**, forming the foundation of all digital systems.

---

## Advantages of Binary Systems

**Simplicity in Hardware:** Uses only two states that directly map to OFF and ON electrical signals.  
**e.g.** A switch represents 0 (OFF) and 1 (ON).

---

**Reliability / Noise Immunity:** Clear separation between two states makes systems resistant to voltage noise.  
**e.g.** 4.9V is reliably interpreted as 1, while 0.1V is interpreted as 0.

---

**Ease of Logical Operations:** Binary aligns naturally with Boolean logic used in digital circuits.  
**e.g.** AND, OR, and NOT gates operate directly on binary values.

---

**Compact Data Representation:** Large amounts of information can be stored efficiently using bits.  
**e.g.** An 8-bit byte represents 256 values (0–255).

---

**Universality in Computing:** Binary can encode numbers, text, and instructions.  
**e.g.** ASCII uses binary patterns to represent characters.

---

## Disadvantages of Binary Systems

Binary systems are ideal for machines but introduce limitations when used by humans.

---
## Disadvantages of Binary Systems

**Hard for Humans:** Binary numbers are long and difficult to read.  
**e.g.** 255₁₀ → 11111111₂

---

**High Bit Count:** Large numbers require many bits for representation.  
**e.g.** 1023₁₀ → 1111111111₂

---

**Resource Overhead:** Binary may consume more memory or bandwidth than decimal-based formats.

---

**Manual Arithmetic:** Calculations are harder to perform accurately.  
**e.g.** 101101 + 11011 requires careful bit-by-bit addition.

## Binary Number Code Categories

Binary representation extends beyond pure numbers into structured codes used for storage, communication, and control.

| Category | Examples | Purpose |
|--------|----------|---------|
| **Pure Binary Codes** | Natural Binary | Standard base-2 representation |
| **Weighted Codes** | BCD (8421), Excess-3 | Decimal digit encoding |
| **Non-Weighted Codes** | Gray, Johnson | Error reduction, counters |
| **Alphanumeric Codes** | ASCII, Unicode | Text and symbols |
| **Error-Detecting Codes** | Parity, VRC | Error detection |
| **Error-Correcting Codes** | Hamming, CRC | Error detection and correction |
| **Signed Representations** | 2’s Complement | Positive and negative numbers |
| **Special Logic Codes** | Gray, Biquinary | Counters and encoders |

<p align="center">
  <img src="../media/flow.jpg" style="width: 100%; max-width: 800px; height: auto;">
  <br>
  <em>Figure 1: Classification of Binary Number Codes</em>
</p>

---

flowchart TB
    A[Binary Codes]:::main

    %% Level 1 Categories
    PB[**Pure Binary Codes**\n(e.g., 1010, 1101)]
    WC[**Weighted Codes**\n(e.g., BCD 8421, 5211, Excess-3)]
    NWC[**Non-Weighted Codes**\n(e.g., Gray Code, Johnson Code)]

    %% Level 2 Categories
    ALPHA[**Alphanumeric Codes**\n(e.g., ASCII 'A'=01000001, Unicode '世'=4E16)]
    EDC[**Error-Detecting Codes**\n(e.g., Parity Bits, 1010 → 10101)]
    ECC[**Error-Correcting Codes**\n(e.g., Hamming 7,4, 1011 → 0110011)]

    %% Level 3 Categories
    SNR[**Signed Number Representations**\n(e.g., 2's complement 8-bit: -22 → 11101010)]
    SDC[**Special Digital Logic Codes**\n(e.g., Gray, Biquinary, Ring Counter)]

    %% Connections
    A --> PB
    A --> WC
    A --> NWC

    PB --> ALPHA
    WC --> EDC
    NWC --> ECC

    A --> SNR
    SNR --> SDC

    %% Styling
    classDef main fill:#f2f2f2,stroke:#333,stroke-width:2px;

---
## Binary Codes by Function

| **Function** | **Examples** | **Use** |
|--------------|-------------|---------|
| **Numeric** | Natural Binary, BCD, 2’s Complement | Arithmetic & storage |
| **Error Control** | Parity, Hamming, CRC | Detect & correct errors |
| **Text / Data** | ASCII, Unicode | Letters & symbols |
| **Logic / Counters** | Gray, Johnson, Ring Counter | Digital circuits & counters |

---

<!--
← [Previous: Number Systems Overview](00-Number-Systems.md) | [Next: Binary Number Codes](02-Binary-Codes.md) →
-->
