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

## Memory, Cache, and Virtual Memory

### 1. Locality of Reference
Programs often reuse the same data or nearby instructions. This principle helps cache memory predict which data will be needed next.

#### Types:
- **Temporal Locality (Time):** Recently accessed data is likely to be used again soon.
  - Example: Loops, counters, frequently used variables.
  - Cache stores these for fast repeated access.

- **Spatial Locality (Space):** Accessed memory often has nearby addresses that will be accessed soon.
  - Example: Arrays or sequential instructions.
  - Cache loads a whole block of memory including nearby addresses.

#### Average Memory Access Time (AMAT)
\[
\text{AMAT} = (h \times T_c) + ((1-h) \times T_m)
\]
- \(h\) = cache hit ratio  
- \(T_c\) = time to access cache  
- \(T_m\) = time to access main memory  

---

### 2. Cache Memory
Small, high-speed memory near the CPU to store frequently used data.

**Advantages:**
- Faster data access than RAM.
- Reduces CPU idle time.
- Reduces bottlenecks from slow memory.

**Disadvantages:**
- Limited size.
- Expensive.
- Complex to manage efficiently.

---

### 3. Virtual Memory
Technique allowing programs to use more memory than physically available RAM by using disk storage (swap space).

**How it works:**
- Divides memory into pages (fixed-size) or segments (variable-size).  
- Unused pages/segments are stored on disk; brought into RAM when needed.

**Types:**
1. **Paging:** Fixed-size pages, uses swap file.
2. **Segmentation:** Variable-size segments.

**Effective Memory Access Time (EMAT) with page faults:**
\[
\text{EMAT} = (p \times s) + ((1-p) \times m)
\]
- \(p\) = page fault rate  
- \(s\) = page fault service time  
- \(m\) = main memory access time  

**Advantages:**
- Run programs larger than RAM.
- Multiprogramming.
- Isolates memory for safety.
- Efficient memory management.

**Disadvantages:**
- Slower than RAM.
- Complex management.
- Disk wear with heavy use.

---

### 4. Cache Memory vs Virtual Memory

| Feature | Cache Memory | Virtual Memory |
|---------|--------------|----------------|
| Type | Hardware memory unit | Technique using RAM + disk |
| Purpose | Faster CPU access | More memory than physical RAM |
| Size | Small | Large (disk dependent) |
| Speed | Fast | Slower |
| Managed by | Hardware | Operating system |
| Data Stored | Frequently used data | Program parts not in RAM |
| Mapping | None | Virtual → Physical address |
| Access | Direct from CPU | May involve page swaps from disk |

**Summary:**  
- **Cache:** Makes small memory fast.  
- **Virtual Memory:** Makes big memory available.

---

## Instruction Set Architecture (ISA) and Microarchitecture

### 1. Instruction Set Architecture (ISA)
- **Definition:** The “language” of the CPU; defines what operations the CPU can perform and how software communicates with hardware.
- **Examples:** x86 (PCs), ARM (phones), MIPS (education), RISC-V (open source).
- **Main Components:**
  1. **Instruction Types**
     - Arithmetic/Logic: ADD, SUB, AND, OR
     - Data Transfer: LOAD, STORE
     - Branch/Jump: loops, function calls
  2. **Instruction Length:** Fixed (e.g., 32-bit in MIPS)
  3. **Instruction Formats:**
     - R-type: arithmetic/logic
     - I-type: data transfer & conditional branches
     - J-type: unconditional jumps
- **Importance:**
  - Software compatibility
  - Performance optimization
  - Basis for assembly programming
- **Types of ISA:**
  - RISC: few simple instructions
  - CISC: many complex instructions
  - VLIW/EPIC: multiple operations per instruction
  - Stack-based: uses stack instead of registers

### 2. Microarchitecture
- **Definition:** Internal design of CPU that executes ISA instructions.
- **Components:** ALU, pipelines, cache, control unit, execution units.
- **Analogy:** ISA = recipe, Microarchitecture = kitchen setup.

### 3. Datapath
- **Definition:** Path data takes inside CPU during instruction execution.
- **Components:**
  1. Registers
  2. Register File
  3. ALU (Arithmetic Logic Unit)
  4. Multiplexers (MUX)
  5. Memory
  6. Sign/Zero Extender
  7. Shift Units
  8. Buses
  9. Control Signals

### 4. Datapath Designs
1. **Single-Cycle:** Each instruction completes in one long cycle; simple but slow.
2. **Multi-Cycle:** Instruction split into multiple shorter cycles; more efficient.
3. **Pipelined:** Multiple instructions processed in overlapping stages; high throughput, more complex.

### Key Takeaways
- **ISA:** What CPU can do.
- **Microarchitecture:** How CPU executes instructions internally.
- **Datapath:** Where and how data flows inside CPU.
- **Design trade-offs:** Simplicity vs speed (single, multi-cycle, pipeline).

---

## Direct Memory Access (DMA) & 8257/8237 Controller

**Definition:**  
DMA allows peripheral devices to transfer data directly to/from memory **without CPU involvement**, improving speed and efficiency.

### DMA Operation Steps
1. **DMA Request (DREQ):** Peripheral requests DMA service.  
2. **Bus Control Request (HOLD):** DMA controller asks CPU to release the bus.  
3. **CPU Acknowledgement (HLDA):** CPU grants bus control.  
4. **DMA Acknowledgement (DACK):** DMA controller confirms to peripheral.  
5. **Data Transfer:** DMA controller moves data directly between memory and peripheral.  
6. **Completion:** CPU regains bus control.

### 8257/8237 Features
- 4 independent DMA channels (read/write/verify)  
- Max 64 KB per transfer  
- Single and cascade modes  
- Generates MARK signal every 128 bytes  
- Master and slave modes for flexible configurations  

### DMA Modes
- **Single Mode:** One DMA channel active  
- **Cascade Mode:** Multiple DMA channels chained  

---

## Bus Arbitration

**Definition:**  
Bus arbitration ensures **only one device** controls a shared bus at a time, preventing conflicts and data corruption.

### Key Concepts
- **Bus Master:** Device currently controlling the bus  
- **Arbitration:** Process of selecting the next bus master  
- **Importance:** Maintains system stability and data integrity  

### Types of Arbitration
1. **Centralized:** Single arbiter manages requests  
   - *Daisy Chaining:* Bus grant propagates; first requesting device wins  
2. **Distributed:** Devices compete using IDs; highest priority wins  

### Applications
- Shared memory systems  
- Multi-processor systems  
- I/O devices  
- Real-time systems  
- Embedded systems  

### Advantages
- Efficient use of system resources  
- Minimizes data corruption  
- Supports multiple devices  
- Real-time system support  
- Improves stability  

### Challenges
- Hardware complexity for daisy chaining  
- Priority management in distributed systems

---

## Asynchronous Input/Output (I/O) Synchronization

### Definition
Asynchronous I/O allows data transfer between CPU and external devices **without a fixed clock**, operating independently at variable rates.  
- **Synchronous I/O:** Uses a clock, fixed transfer rate.  
- **Asynchronous I/O:** No clock, transfers occur when data/device is ready.

### Use Cases
- Serial communication  
- Slow or variable-speed devices  
- Interrupt-driven I/O

### Problems
- Data on the bus may not be fresh (no guaranteed timing).

### Mechanisms

#### 1. Strobe Mechanism
**Signals when data is ready:**
- **Source-Initiated:** Source places data → strobe ON → destination reads → strobe OFF  
- **Destination-Initiated:** Destination signals → source puts data → destination reads → strobe OFF  
**Issue:** No certainty that data is read or placed correctly.

#### 2. Handshaking Mechanism
**Ensures proper data transfer:**
- **Source-Initiated:**
  1. Source puts data → **DATA VALID ON**  
  2. Destination reads → **DATA ACCEPTED ON**  
  3. Signals OFF after completion  
- **Destination-Initiated:**
  1. Destination → **REQUEST FOR DATA ON**  
  2. Source places data → **DATA VALID ON**  
  3. Destination reads → signals OFF  

### Features
- Callback functions (CPU notified when transfer completes)  
- Interrupts (CPU handles events immediately)  
- Polling (CPU checks device status)  
- Select function (monitor multiple devices)

### Advantages
- Flexible transfer rates  
- Efficient resource usage  
- Reduced latency  
- Better error handling  
- Wide device compatibility

### Disadvantages
- Complex implementation  
- CPU overhead  
- Potential latency issues  
- Synchronization challenges for multiple devices  
- Compatibility problems with fixed-rate devices

---