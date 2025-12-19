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