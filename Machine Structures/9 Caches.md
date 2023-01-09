# Caches

Caches store what we call "blocks" of the memory

- Blocks are contiguous chunks of memory

when cache is full, if new data then compulsory, otherwise capacity, also can be conflict?

increasing cache size by adding more blocks does not always increase hit rate

### *Hierarchy*

registers ↔ memory *(by compiler)*

<u>cache ↔ main memory *(by the cache controller hardware)*</u>

main memory ↔ disks *(by the operating system (virtual memory) assisted by hardware)*

## T / I / O

| Tag                                                          | Index                                                      | Offset                                       |
| ------------------------------------------------------------ | ---------------------------------------------------------- | -------------------------------------------- |
| Used to distinguish different <u>blocks</u> that use the same index | The <u>set</u> that this piece of memory will be placed in | The location of the <u>byte</u> in the block |
| num bits = # bits in memory address - Index Bits - Offset Bits | num bits = log2 (# of indices)                             | num bits = log2 (size of block)              |

### Equations

- *log2(memory size) = address bit-width = # tag bits + # index bits + # offset bits*
- **cache size = block size * num blocks** (A = H * W)
- N-way associative cache: **N * # sets = # blocks**
  - direct-mapped: N = 1, fully-associative: N = M
  - each set has N elements

### Why TIO

- **ITO:** index bits won't change very often, so low associativity → high conflicts (**0**00, **0**01, **0**10, **0**11)
- **TOI:** index will change a lot, so lose benefit of bringing in cache blocks → contiguous would map to diff indices (00**0**, 00**1**)

## Types of Caches

|         | Direct Mapped                                                | Fully Associative                                 | N-way Set Associative                                        |
| ------- | ------------------------------------------------------------ | ------------------------------------------------- | ------------------------------------------------------------ |
| add     | every memory address is associated with one possible "block" within the cache | data blocks go anywhere → the next available spot | consists of M sets with N blocks in each set *(can go in either slot in set)*; |
| pros    | quick access to cache                                        | fewer conflict misses                             | each maps into a specific set, similar to DM and the blocks within a set are used based on FA |
| cons    | a lot of conflict misses                                     | slower accesses                                   |                                                              |
| replace | index completely specifies which position a block can go in  | block can be written into any position            | index specifies a set, block can occupy any position within set |

## Calculating Size

2^XY^ (2^34^ = 16 gibi)

| Name | Abbr | IEC Factor |
| ---- | ---- | ---------- |
| kibi | Ki   | 2^10^      |
| mebi | Mi   | 2^20^      |
| gibi | Gi   | 2^30^      |
| tebi | Ti   | 2^40^      |
| pebi | Pi   | 2^50^      |
| exbi | Ei   | 2^60^      |
| zebi | Zi   | 2^70^      |
| yobi | Yi   | 2^80^      |

## Cache Misses

**cache hit:** block is valid and contains proper address, read desired word

**cache miss:** nothing in cache in appropriate block, fetch from memory

**cache miss, block replacement:** wrong data in appropriate block, discard it and fetch desired from memory

| Compulsory                                          | Conflict                                                     | Capacity                                                     |
| --------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| first access to a block *(cold)*                    | cache cannot contain all blocks accessed by the program      | multiple memory locations mapped to the same cache location; independent of the associativity |
|                                                     | running fully associative cache: <u>is not a miss</u> for that specific access | running fully associative cache: <u>is a miss</u> for that specific access |
| reduce by having longer cache lines (bigger blocks) | increasing associativity or improving the replacement policy would remove the miss | remove this miss by increasing cache capacity                |

*(Algorithm lec26-slide39: checking whether it's a conflict or capacity cache miss: if hypothetically, you ran the ENTIRE string of memory accesses with a fully associative cache of the same size as your cache…)*

## Other

**Temporal Locality:** if accessing <u>similar memory addresses over time</u>, for example going through an array multiple times

**Spatial Locality:** if accessing <u>contiguously</u> in memory, instead of bringing in one byte, we can bring in a bunch together

**Replacement Policies:** <u>LRU</u> (Least Recently Used), <u>RR</u> (Random Replacement)

**Cache Coherency:** <u>Write-through</u> (instant update both cache and memory), <u>Write-back</u> (mark block as dirty, update RAM when a cache block is kicked out)

## Cache Example

### Steps

1. Look at <u>index</u>
2. Check if <u>tag</u> matches

### <u>Direct-Mapped Byte-addressed Cache</u>

address 32B, capacity 32B, block size 8B

**cache size = block size * num blocks**

- 32B = 8B * <u>4 blocks</u> (2^2^) ⟶ **2 bits for index**
- 8B (2^3^) block size ⟶  **3 bits for offset**
- 32 - 3 - 2 ⟶ **27 bits for tag**

|      | Address    | T/I/O            | Hit, Miss, Replace | T/I    |
| ---- | ---------- | ---------------- | ------------------ | ------ |
| 1    | 0x00000004 | …0000 / 00 / 100 | M (compulsory)     | 000000 |
| 2    | 0x00000005 | …0000 / 00 / 101 | H                  | 000000 |
| 3    | 0x00000068 | …0011 / 01 / 000 | M (compulsory)     | 001101 |
| 4    | 0x000000C8 | …0110 / 01 / 000 | R (compulsory)     | 011001 |
| 5    | 0x00000068 | …0011 / 01 / 000 | R (conflict)       | 001101 |
| 6    | 0x000000DD | …0110 / 11 / 101 | M (compulsory)     | 011011 |
| 7    | 0x00000045 | …0010 / 00 / 101 | R (compulsory)     | 001000 |
| 8    | 0x00000004 | …0000 / 00 / 100 | R (capacity)       | 000000 |
| 9    | 0x000000C8 | …0110 / 01 / 000 | R (capacity)       | 011001 |

Process

| Index | Tag                       |
| ----- | ------------------------- |
| 00    | 0000 → 0010 → 0000        |
| 01    | 0011 → 0110 → 0011 → 0110 |
| 10    | 0110 1100                 |
| 11    | 0110                      |

Fully Associative Cache (to identify <u>conflict type</u>)

| Tag (T/I)           |      |
| ------------------- | ---- |
| 000000 → 001000 (7) | ~    |
| 001101 → 011001 (9) | ~    |
| 011001 → 000000 (8) | ~    |
| 011011              | ~    |

Cache - 2 bit <u>index</u> **by** 3 bit <u>offset</u>

|        | **000** | **001** | **010** | **011** | **100** | **101** | **110** | **111** |
| ------ | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| **00** |         |         |         |         |         |         |         |         |
| **01** |         |         |         |         |         |         |         |         |
| **10** |         |         |         |         |         |         |         |         |
| **11** |         |         |         |         |         |         |         |         |

### <u>N-way Associative Cache</u>

2-way set associative - address space 8B, cache size 32B, block size 8B

**N * # sets = # blocks** → **# sets = # blocks / N** → **# sets = (cache size / block size) / N**

- 8B (2^3^) block size ⟶  **3 bits for offset**
- num sets = log((32/8)/2) ⟶  **1 bit for index**
- 8 - 3 - 1 ⟶  **4 bit for tag**

|      | Address     | T/I/O           | Hit, Miss, Replace | T/I   |
| ---- | ----------- | --------------- | ------------------ | ----- |
| 1    | 0b0000 0100 | …0000 / 0 / 100 | M (compulsory)     | 00000 |
| 2    | 0b0000 0101 | …0000 / 0 / 101 | H                  | 00000 |
| 3    | 0b0110 1000 | …0110 / 1 / 000 | M (compulsory)     | 01101 |
| 4    | 0b1100 1000 | …1100 / 1 / 000 | M (compulsory)     | 11001 |
| 5    | 0b0110 1000 | …0110 / 1 / 000 | H                  | 01101 |
| 6    | 0b1101 1101 | …1101 / 1 / 101 | R (compulsory)     | 11011 |
| 7    | 0b0100 0101 | …0100 / 0 / 101 | M (compulsory)     | 01000 |
| 8    | 0b0000 0100 | …0000 / 0 / 100 | H                  | 00000 |
| 9    | 0b1100 1000 | …1100 / 1 / 000 | R (capacity)       | 11001 |

Process

| Index | Tag                 |
| ----- | ------------------- |
| 0     | 0000 (1)            |
| 0     | 0100 (7)            |
| 1     | 0110 (3) → 1100 (9) |
| 1     | 1100 (4) → 1101 (6) |

Hit Rate:

- **hits/total** = 3/9 = 1/3

Fully Associative Cache (to identify <u>conflict type</u>)

| Tag (T/I)         |      |
| ----------------- | ---- |
| 00000 → 01000 (7) | ~    |
| 01101 → 11001 (9) | ~    |
| 11001 → 00000 (8) | ~    |
| 11011             | ~    |

## Cache Example (Guerilla)

### <u>Direct Mapped - Replacing Blocks</u>

8-bit system, 32B cache, 2-word block

- 8B block ⟶  **3 bits for offset**
- num blocks = 4 ⟶  **2 bits for index**
- 8 - 3 - 2 ⟶  **3 bits for tag**

|      | Address | T/I/O          | Notes               |
| ---- | ------- | -------------- | ------------------- |
| 1    | 0xAC    | 101 / 01 / 100 | block1              |
| 2    | 0x18    | 000 / 11 / 000 | block3              |
| 3    | 0xF6    | 111 / 10 / 110 | block2              |
| 4    | 0x44    | 010 / 00 / 100 | block0 (full cache) |
| 5    | 0x9A    | 100 / 11 / 010 | evict block 3       |
| 6    | 0x3A    | 001 / 11 / 010 | evict block 3       |
| 7    | 0xE4    | 111 / 00 / 100 | evict block 0       |
| 8    | 0x00    | 000 / 00 / 000 | evict block 0       |

*brings in the whole cache block with it*

| Index      | 0                      | 1                  | 2                          | 3                  | 4                          | 5                  | 6                  | 7                  |
| ---------- | ---------------------- | ------------------ | -------------------------- | ------------------ | -------------------------- | ------------------ | ------------------ | ------------------ |
| **Block0** | 0x40 → 0xE0 → **0x00** | 0x41 → 0xE1 → 0x01 | 0x42 → 0xE2 → 0x02         | 0x43 → 0xE3 → 0x03 | **0x44** → **0xE4** → 0x04 | 0x45 → 0xE5 → 0x05 | 0x46 → 0xE6 → 0x06 | 0x47 → 0xE7 → 0x07 |
| **Block1** | 0xA8                   | 0xA9               | 0xAA                       | 0xAB               | **0xAC**                   | 0xAD               | 0xAE               | 0xAF               |
| **Block2** | 0xF0                   | 0xF1               | 0xF2                       | 0xF3               | 0xF4                       | 0xF5               | **0xF6**           | 0xF7               |
| **Block3** | **0x18** → 0x98 → 0x38 | 0x19 → 0x99 → 0x39 | 0x1A → **0x9A** → **0x3A** | 0x1B → 0x9B → 0x3B | 0x1C → 0x9C → 0x3C         | 0x1D → 0x9D → 0x3D | 0x1E → 0x9E → 0x3E | 0x1F → 0x9F → 0x3F |

### <u>Comparing 3 Cache Performances (Miss Rate)</u>

| Cache | Type                                                 | T/I/O                       |
| ----- | ---------------------------------------------------- | --------------------------- |
| 1     | direct-mapped, 4 blocks, 4B block                    | tag: x, index: 2, offset: 2 |
| 2     | 2-way set associative (LRU), 16B capacity, 4B blocks | tag: x, index: 1, offset: 2 |
| 3     | fully associative (LRU), 16B capacity, 4B blocks     | tag: x, index: 2, offset: 2 |

Memory to Cache

| Memory Address | Cache 1 T/I/O       | Cache 2 T/I/O       |
| -------------- | ------------------- | ------------------- |
| 32             | …0010 / **00** / 00 | …00100 / **0** / 00 |
| 16             | …0001 / **00** / 00 | …00010 / **0** / 00 |
| 12             | …0000 / **11** / 00 | …00001 / **1** / 00 |
| 8              | …0000 / **10** / 00 | …00001 / **0** / 00 |
| 4              | …0000 / **01** / 00 | …00000 / **1** / 00 |
| 0              | …0000 / **00** / 00 | …00000 / **0** / 00 |

Miss Rates:

| Memory Accesses                                              | Cache 1                              | Cache 2                                   | Cache 3                                          |
| ------------------------------------------------------------ | ------------------------------------ | ----------------------------------------- | ------------------------------------------------ |
| **0, 4, 0, 4, …** (first 4 compulsory M then inf hits; indices 00, 01) | **0%**                               | **0%**                                    | **0%**                                           |
| **0, 16, 32, 0, 16, 32, …** (index = 0)                      | **100%** (always evicts at index 00) | **100%** (always evicts an index 0 block) | **0%**                                           |
| **0, 4, 8, 12, 16, 0, 4, 8, 12, 16, …** (first 4 compulsory M) | **40%** (16 R 0, 0 R 16)             | **60%** (16 R 0, 0 R 8, 8 R 16)           | **100%** (16 R 0, 0 R 4, 4 R 8, 8 R 12, 12 R 16) |
| **0, 4, 8, 12, 16, 12, 8, 4, 0, …**                          | **40%** (16 R 0, 0 R 16)             | **40%** (16 R 0, 0 R 16)                  | **40%** (16 R 0, 0 R 16)                         |



## Average Memory Access Time (AMAT)

want to minimize **AMAT = Hit Time + Miss Rate * Miss Penalty**

- **Hit time:** the time for the cache to access memory (verify our data exists in the cache)
- **Miss Penalty:** the time taken to get our data from memory (or the next level cache) when we miss
- **Miss Rate:** the number of accesses that missed at that level / total number of accesses…
  1. Global: *to the cache system*
  2. Local: *to the cache level*
- <u>Multi-level:</u> AMAT = L1 Hit Time + L1 Miss Rate * (L2 Hit Time + L2 Miss Rate * L2 Miss Rate)
- <u>Paging Impact:</u> *take a look at hw!*

<u>Improve AMAT:</u>

1. Decreasing cache "Hit time"
2. Reduce miss rate
3. Reduce miss penalty

### Example

if L2$: miss 20 / 100 total accesses ⟶ L2% global miss rate = 20%

if L1$: 50% miss rate ⟶ L2$ local miss rate = 20% / 50% = 40%

**Then suppose:**

- L1$ with hit time of 2 cycles, local miss rate of 20%
- L2$ with hit time of 15 cycles, global miss rate of 5%
- main memory where accesses take 100 cycles

L2$ local miss rate

- #L2 misses / #L2 accesses = 5/20 = 25%

AMAT of the system

- hit time + miss rate * miss penalty
- 2 + 0.2 (15 + 0.25 (100)) = 10 cycles

Largest L3$ hit time - if we want 8 cycles or lower by adding an L3$ with miss rate of 30%

- 8 >= 2 + 0.2 (15 + 0.25 (**X** + 0.3(100)))
- **X** <= 30 cycles

