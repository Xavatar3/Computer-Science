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

**Example**  
  - **Main memory:** 64 blocks  
  - **Cache size:** 8 lines  
  - **Block size:** 1 word  
  - **Cache lines** = 8  

**Direct Mapping**
  - **Rule:** `Cache Line = Block Number MOD Number of Cache Lines`  
  - **Example:** Block 26 → `26 MOD 8 = 2` → Cache Line 2  
  - **Issue:** Block 34 → `34 MOD 8 = 2` → replaces Block 26 → **conflict miss**  

**Fully Associative Mapping**  
- **Rule:** Any block can go into **any cache line**  
- **Example:** Block 26 → any line, Block 34 → any free line  

**Set-Associative Mapping (2-way)**  
- **Setup:** 8 cache lines ÷ 2-way = 4 sets, each with 2 lines  
- **Rule:** `Set Number = Block Number MOD Number of Sets`  
- **Example:**  
  - Block 26 → `26 MOD 4 = 2` → Set 2 (can use either line)  
  - Block 34 → `34 MOD 4 = 2` → Set 2 (can use the other line)  

**Mental Picture**  
- **Direct Mapping:** Each car has one fixed parking spot.
- **Fully Associative:** Any car can park anywhere.
- **Set-Associative:** Cars park in a specific section but choose any spot inside it.

---

## CPU Input/Output (I/O)  
The CPU communicates with memory and peripheral devices (I/O) using the system bus. There are two main methods for handling I/O: Isolated I/O and Memory-Mapped I/O.

### System Bus  
A bus is a bundle of wires carrying information. A system bus is actually made up of three separate buses  
- **Address bus:** Which location/device to access (“Where?”)  
- **Data bus:** The actual data (“What?”)  
- **Control bus:** Type of operation (“Read/Write” and whether it’s memory or I/O)  

**NB:** I/O refers to the devices like monitor and keyboard.  

### Terms  
**1. Contention**  
  - **Defn:** This is when two or more devices or instructions try to use the same hardware resource at the same time, causing a delay or conflict.  
  - **Example:** Two I/O devices try to write to the data bus simultaneously. The CPU must wait or arbitrate which device goes first.  
  - **Effects:**  
    - Can slow down the system  
    - Requires resource scheduling or bus arbitration to resolve  

**2. Address Space**
  - **Definition:** Address space is the range of unique addresses that a CPU or device can use to access memory or I/O devices.  
  - **Types:**  
    - **Memory Address Space:** All addresses that can point to memory locations.  
    - **I/O Address Space:** All addresses reserved for I/O ports/devices.  
    - **Example:**  
      - If a CPU has a 16-bit address bus for memory, the memory address space is `0x0000` to `0xFFFF` (65,536 addresses).  
      - In isolated I/O, I/O devices have a separate address space from memory.  
    - **Effect:**  
      - Determines how much memory or how many devices a CPU can access.  
      - Helps organize memory and I/O mapping efficiently.

### Isolated I/O
- Memory and I/O have separate address spaces.  
- The CPU uses special instructions (e.g., `IN`/`OUT`) to access I/O.  
- Separate control signals (`IO_READ`, `IO_WRITE`) tell devices to respond.  

**How it works**  
1. CPU puts the port address on the address bus  
2. CPU asserts IO control signals  
3. Only the targeted I/O device responds on the data bus  
4. Memory ignores these signals

**Advantages**  
- Large I/O address space  
- Greater flexibility in adding/removing devices  
- Improved reliability, as memory is not affected by I/O failures

**Disadvantages**  
- Slower operations due to extra instructions  
- Programming is more complex  

**Applications**  
- Embedded systems (robots, industrial controls)  
- Microcontrollers interfacing multiple peripherals  
- Real-time systems requiring strict timing  

### Memory-Mapped I/O

In Memory-Mapped I/O:  
- I/O devices share the same address space as memory  
- CPU uses normal memory instructions (`LOAD`, `STORE`)  
- Devices behave electrically like memory chips

**How it works**  
1. CPU puts a memory-mapped address on the address bus  
2. Control bus signals a normal memory read/write  
3. The corresponding device responds as if it were a memory cell

**Advantages**  
- Faster I/O operations (same as memory access)  
- Simplified programming (no special I/O instructions)  
- Efficient use of address space  

**Disadvantages**  
- Limited I/O address space (shares memory)  
- Slow device response can delay CPU  
- Must carefully manage caching  

**Applications**  
- Graphics cards (framebuffers)  
- Network interface cards (NICs)  
- Direct Memory Access (DMA) devices  

### Key Physical Concepts

- **Address decoding:** Logic circuits determine which memory or I/O device responds to a given address  
- **Control signals:** Tell devices whether it’s a read or write operation  
- **Bus contention:** Only one device can drive the data bus at a time; arbitration is needed for DMA  
- **Timing:** CPU may need wait states if devices are slower than RAM  
- **Caching:** Memory-mapped I/O regions are often marked non-cacheable to avoid stale reads  

### Isolated vs Memory-Mapped I/O

| Feature | Isolated I/O | Memory-Mapped I/O |
|:---------|:--------------|:-----------------|
| Address space | Separate | Shared with memory |
| Control signals | Special (`IN/OUT`, `IO_READ/WRITE`) | Normal memory signals (`READ/WRITE`) |
| Instruction set | Different for memory and I/O | Same as memory instructions |
| Hardware complexity | More wires & logic | Simpler, fewer wires |
| CPU perspective | “Different world for I/O” | “I/O is memory” |
| Speed | Slightly slower | Potentially faster (depends on device) |  

---