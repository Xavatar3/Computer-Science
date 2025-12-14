---

## Binary-Coded Decimal (BCD) Codes

---

### Definition
Binary-Coded Decimal (BCD) is a code that represents decimal digits (0–9) using 4-bit binary codes. Each decimal digit is encoded separately.  

| Variant | Mapping(0–9) | Notes |
|:------------|:-------------------------:|:-----------|
| 8421 BCD   | 0000–1001               | Standard BCD, straightforward weights |
| 5211 BCD   | 0000–1001               | Self-complementing; easier subtraction |
| 2421 BCD   | 0000–1001               | Self-complementing; Aiken code |
| Excess-3   | 0011–1100               | Self-complementing; each digit +3; simplifies subtraction |

  _Table 1: BCD Variants_  

***Note:*** Since a 4-bit code can represent up to 1111 (15 in decimal), each BCD variant uses only 10 of the 16 possible combinations (for digits 0–9). This leaves six unused or illegal codes in each BCD system.

---

### Uses
BCD is widely used in digital clocks, calculators, and display systems.  
- Representing decimal numbers in digital circuits.  
- Displaying numbers on seven-segment displays.  
- Performing decimal arithmetic in computers and calculators.

---

### Characteristics  
- 4 bits per decimal digit.  
- Multiple variants exist based on positional weighting  
- Arithmetic requires adjustment logic after binary addition for digits >9.

---

### Advantages
- Easy to display decimal numbers directly.  
- Certain variants are self-complementing, simplifying subtraction.  
- Well-suited for decimal-centric applications.

---

### Disadvantages
- Requires more bits than pure binary for the same number.  
- Arithmetic is less efficient; extra logic needed for carry and correction.  
- Not ideal for large-scale numeric computation compared to straight binary.

---