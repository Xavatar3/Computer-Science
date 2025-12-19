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

---

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