## Instruction Cycle
The **instruction cycle** is the continuous process a CPU follows to execute a program.  
### Steps of the Instruction Cycle

- **Fetch:** The CPU retrieves the next instruction from memory:  
  - **Program Counter (PC):** Holds (points to) the address of the next instruction.  
  - **Memory Address Register (MAR):** The memory address(location) is placed in **MAR** to tell memory where to look.  
  - **Memory Data Register (MDR):** Holds the data (or the instruction fetched) read from Memory before it is sent to IR.  
  - **Instruction Register (IR):** Receives the instruction(from MDR) for decoding. After fetching, the Program Counter automatically goes to the next instruction.

- **Decode:** The control unit interprets the instruction in the IR, determining the operation and the resources required.

- **Execute:** The CPU performs the operation using the ALU and relevant registers, such as calculations, data movement, or memory access.

### Key Points

- The cycle repeats millions or billions of times per second.  
- Ensures instructions are processed in a clear, orderly manner.  
- The Registers (PC, IR, MAR, MDR) work together to maintain efficiency and accuracy.  
- The MDR stores **data** it temporarily before its sent to the IR as instructions.  

---

### Challenges in Modern CPU Instruction Execution

**1. Pipeline Hazards:** Pipelining overlaps instruction execution to increase speed. Hazards occur when:
- An instruction needs a result that hasn't been produced yet.(**data hazards**).
- A branch changes the control flow and the cpu doesn't know which instruction comes next (**control hazards**).
- Two instructions need the same hardware at the same time (**structural hazards**).

These hazards cause stalls or bubbles in the pipeline, reducing performance.

**2. Branch Prediction Errors:** Correct predictions improve speed while Incorrect predictions require fetching the correct path. This wastes cycles and lowers efficiency.

**3. Instruction Cache Misses:** Missing instructions in the cache must be fetched from slower main memory causing delays. 

**4. Instruction-Level Parallelism (ILP) Limitations** ILP allows multiple instructions to execute simultaneously but has limitations.
- Data dependencies and control flow limit parallelism.
- Not all instructions can run in parallel.

**5. Resource Contention**
Multiple instructions may compete for the same CPU resources (ALUs, registers, memory ports) causing stalls thus slowing execution.

---

## Cache Mapping  
A technique that determines where a block of main memory is stored in the cache.  

### Terminologies  
- **Cache memory:** A small, high-speed memory used to reduce the speed gap between the CPU and main memory (RAM).  
- **Main Memory Blocks:** Fixed-size divisions of main memory.
- **Cache Lines (Blocks):** Fixed-size divisions of cache memory.
- **Block Size:** Size of each block or cache line.
- **Tag Bits:** Identify which memory block is stored in a cache line.
- **Number of Cache Lines:** `Cache Size ÷ Block Size`
- **Number of Cache Sets:** `Number of Cache Lines ÷ Associativity`

### Types of Cache Mapping  
**1. Direct Mapping:**  
- Each memory block maps to one specific cache line.
- Address is divided into:
  - Tag
  - Line Number
  - Byte Offset
- **Formula:** `Cache Line = Block Number MOD Number of Cache Lines`  
- **Pros:** Fast access, simple hardware  
- **Cons:** High conflict misses, low flexibility

**2. Fully Associative Mapping**  
- A memory block can be placed in any cache line.
- Address is divided into:
  - Tag
  - Byte Offset
- **Pros:** No conflict misses, high flexibility  
- **Cons:** Expensive hardware, slower lookup

**3. Set-Associative Mapping**  
- Cache is divided into sets; each set has multiple lines.
- A block maps to **one set**, but can be placed in **any line within that set**.
- Address is divided into:
  - Tag
  - Set Number
  - Byte Offset
- **Formula:** `Set Number = Block Number MOD Number of Sets`
- **Pros:** Balanced performance and cost  
- **Cons:** More complex than direct mapping

**Why Cache Mapping is Needed**
- Quickly locate data in cache.
- Decide where to place new data after a cache miss.
- Improve overall CPU performance.

**Comparison of Cache Mapping Techniques**
| Feature | Direct Mapping | Fully Associative | Set-Associative |
|-------|---------------|------------------|----------------|
| Placement | Fixed line | Any line | Any line within a set |
| Hardware Cost | Low | High | Moderate |
| Access Time | Fast | Slow | Moderate |
| Conflict Misses | High | None | Low |
| Flexibility | Low | High | Medium |

**Analogy**
- **Direct Mapping:** Each car has one fixed parking spot.
- **Fully Associative:** Any car can park anywhere.
- **Set-Associative:** Cars park in a specific section but choose any spot inside it.

---