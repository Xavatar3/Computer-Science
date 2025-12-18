## Instruction Cycle

The **instruction cycle** is the CPU’s repeating loop for executing programs, consisting of three main steps: **fetch**, **decode**, and **execute**.

### Steps of the Instruction Cycle

- **Fetch**  
  The CPU retrieves the next instruction from memory:  
  - **Program Counter (PC):** Holds (points to) the address of the next instruction.  
  - **Memory Address Register (MAR):** The memory address(location) is placed in **MAR** to tell memory where to look.  
  - **Memory Data Register (MDR):** Holds the data (or the instruction fetched) read from Memory before it is sent to IR.  
  - **Instruction Register (IR):** Receives the instruction(from MDR) for decoding. After fetching, the Program Counter automatically goes to the next instruction.

- **Decode**  
  The control unit interprets the instruction in the IR, determining the operation and the resources required.

- **Execute**  
  The CPU performs the operation using the ALU and relevant registers, such as calculations, data movement, or memory access.

The **Memory Data Register (MDR)** and **Instruction Register (IR)** work together during the instruction cycle, but they serve different purposes. Understanding the difference is crucial because confusion can be misleading: the MDR holds the instruction **as data** before it moves to the IR.

### Key Points

- The cycle repeats millions or billions of times per second.  
- Ensures instructions are processed in a clear, orderly manner.  
- The Registers (PC, IR, MAR, MDR) work together to maintain efficiency and accuracy.  
- An instruction is also **data**. The MDR stores it temporarily before the IR starts decoding it.  

---



---