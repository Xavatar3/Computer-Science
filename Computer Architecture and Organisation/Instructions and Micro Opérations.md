## Instruction Cycle: Fetch, Decode, Execute

The instruction cycle consists of three main stages: **Fetch**, **Decode**, and **Execute**. Each stage ensures the CPU processes instructions efficiently.

### 1. Fetch Cycle
The CPU retrieves the instruction from memory.

**Steps:**
1. **PC → MAR:** The Program Counter provides the address of the next instruction.  
2. **Memory → MDR:** Memory sends the instruction to the **Memory Data Register (MDR)**.  
3. **MDR → IR:** The instruction is transferred to the **Instruction Register (IR)**.  
4. **PC incremented:** PC is updated to point to the next instruction.  

### 2. Decode Cycle
The CPU interprets the instruction stored in the IR.

**Steps:**
1. The **Control Unit** examines the opcode.  
2. Determines the operation to perform.  
3. Identifies operands or registers involved.  

**Note:** The decode cycle only interprets the instruction. The actual operation is performed during the execute cycle.

### 3. Execute Cycle
The CPU performs the operation specified by the instruction.

**Steps:**
- The **ALU** performs arithmetic or logic operations.  
- Data is moved between memory and registers.  
- Execution flow may change (e.g., jump instructions).  

### Overall Example

**Instruction:** `LOAD 500`  

**a) Fetch Cycle**  
1. **PC → MAR:** Suppose `PC = 100`. The CPU sends 100 to MAR to fetch the instruction.  
2. **Memory → MDR:** Memory reads the instruction at address 100 (`LOAD 500`) into MDR.  
3. **MDR → IR:** Instruction `LOAD 500` is transferred to IR.  
4. **PC incremented:** PC now becomes 101 for the next instruction.  

**State:**  
- Before fetch: `PC = 100`  
- After fetch: `IR = LOAD 500`, `PC = 101`  

**b) Decode Cycle**  
- `IR = LOAD 500` → Opcode = `LOAD`, Operand = `500`  
- **Interpretation:** “Take the data stored at memory address 500 and load it into the accumulator.”

**c) Execute Cycle**  
- CPU accesses memory at address 500, retrieves the data (e.g., 42), and loads it into the **accumulator**.  

**State after execution:**  
- `Accumulator = 42`  
- CPU returns to the fetch cycle for the next instruction.  

**Note:** An **accumulator** is a special register that temporarily holds data being worked on, especially intermediate results of arithmetic or logic operations.

### Summary
The example shows how an instruction moves from memory into the CPU and gets executed:  
1. Instruction is **fetched** as data into MDR → IR.  
2. Instruction is **decoded** to understand the operation.  
3. CPU **executes** the instruction, moving actual data into the accumulator.