# Caches

Caches store what we call "blocks" of the memory

- Blocks are contiguous chunks of memory

when cache is full, if new data then compulsory, otherwise capacity, also can be conflict?

increasing cache size by adding more blocks does not always increase hit rate

## T / I / O

| Tag                                                          | Index                                               | Offset                                |
| ------------------------------------------------------------ | --------------------------------------------------- | ------------------------------------- |
| Used to distinguish different blocks that use the same index | The set that this piece of memory will be placed in | The location of the byte in the block |
| num bits = # bits in memory address - Index Bits - Offset Bits | num bits = log2 (# of indices)                      | num bits = log2 (size of block)       |

### Equations

- *log2(memory size) = address bit-width = # tag bits + # index bits + # offset bits*
- **cache size = block size * num blocks**
- N-way associative cache: **N * # sets = # blocks**
  - direct-mapped: N = 1
  - each set has N elements

### Why TIO

- **ITO:** index bits won't change very often, so low associativity → high conflicts (**0**00, **0**01, **0**10, **0**11)
- **TOI:** index will change a lot, so lose benefit of bringing in cache blocks → contiguous would map to diff indices (00**0**, 00**1**)

## Types of Caches

| Direct Mapped                                                | Fully Associative                                 | N-way Set Associative                                        |
| ------------------------------------------------------------ | ------------------------------------------------- | ------------------------------------------------------------ |
| every "block" in memory maps into a specific slot in the cache *(hashing)* | data blocks go anywhere → the next available spot | consists of M sets with N blocks in each set *(can go in either slot in set)*; |
| pro: quick access to cache                                   | pro: fewer conflict misses                        | each maps into a specific set, similar to DM and the blocks within a set are used based on FA |
| con: a lot of conflict misses                                | con: slower accesses                              |                                                              |

## Calculating Size

2^XY^ means

| X = 0     | ---          | IEC   | Y = 0     | 1       |
| --------- | ------------ | ----- | --------- | ------- |
| **X = 1** | kibi ~10^3^  | 2^10^ | **Y = 1** | **2**   |
| **X = 2** | mebi ~10^6^  | 2^20^ | **Y = 2** | **4**   |
| **X = 3** | gibi ~10^9^  | 2^30^ | **Y = 3** | **8**   |
| **X = 4** | tebi ~10^12^ | 2^40^ | **Y = 4** | **16**  |
| **X = 5** | pebi ~10^15^ | 2^50^ | **Y = 5** | **32**  |
| **X = 6** | exbi ~10^18^ | 2^60^ | **Y = 6** | **64**  |
| **X = 7** | zebi ~10^21^ | 2^70^ | **Y = 7** | **128** |
| **X = 8** | yobi ~10^24^ | 2^80^ | **Y = 8** | **256** |
|           |              |       | **Y = 9** | **512** |

## Cache Misses

| Compulsory                                          | Conflict                                                     | Capacity                                                     |
| --------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| first access to a block *(cold)*                    | cache cannot contain all blocks accessed by the program      | multiple memory locations mapped to the same cache location; independent of the associativity |
|                                                     | running fully associative cache: <u>is not a miss</u> for that specific access | running fully associative cache: <u>is a miss</u> for that specific access |
| reduce by having longer cache lines (bigger blocks) | increasing associativity or improving the replacement policy would remove the miss | remove this miss by increasing cache capacity                |

*(checking whether it's a conflict or capacity cache miss: if hypothetically, you ran the ENTIRE string of memory accesses with a fully associative cache of the same size as your cache…)*

## Other

**Cache Blocking:** 

**Temporal Locality:** if accessing similar memory addresses over time, for example going through an array multiple times

**Spatial Locality:** if accessing contiguously in memory, instead of bringing in one byte, we can bring in a bunch together

**Replacement Policies:** LRU (Least Recently Used), RR (Random Replacement)

**Cache Coherency:** Write-through (Instant Update), Write-back (mark block as dirty, update RAM when a cache block is kicked out)

## Cache Example (Disc)

### Steps

1. Look at <u>index</u>
2. Check if <u>tag</u> matches

### <u>Direct-Mapped Byte-addressed Cache</u>

address 32B, capacity 32B, block size 8B

**cache size = block size * num blocks**

- 32B = 8B * <u>4 blocks</u> (2^2^) ⟶ **2 bits for index**
- 8B (2^3^) block size ⟶  **3 bits for offset**
- 32 - 3 - 2 ⟶ **27 bits for tag**

|      | Address    | T/I/O            | Hit, Miss, Replace |      |
| ---- | ---------- | ---------------- | ------------------ | ---- |
| 1    | 0x00000004 | …0000 / 00 / 100 | M                  |      |
| 2    | 0x00000005 | …0000 / 00 / 101 | H                  |      |
| 3    | 0x00000068 | …0011 / 01 / 000 | M                  |      |
| 4    | 0x000000C8 | …0110 / 01 / 000 | R                  |      |
| 5    | 0x00000068 | …0011 / 01 / 000 | R                  |      |
| 6    | 0x000000DD | …0110 / 11 / 101 | M                  |      |
| 7    | 0x00000045 | …0010 / 00 / 101 | R                  |      |
| 8    | 0x00000004 | …0000 / 00 / 100 | R                  |      |
| 9    | 0x000000C8 | …0110 / 01 / 000 | R                  |      |

Process

| Index | Tag                       |
| ----- | ------------------------- |
| 00    | 0000 → 0010 → 0000        |
| 01    | 0011 → 0110 → 0011 → 0110 |
| 10    | 0110 1100                 |
| 11    | 0110                      |

Fully Associative Cache (to identify <u>conflict type</u>)

| Tag (T/I)       |      |
| --------------- | ---- |
| 000000 → 001000 | ~    |
| 001101 → 011001 | ~    |
| 011001 → 000000 | ~    |
| 011011          | ~    |

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

|      | Address     | T/I/O           | Hit, Miss, Replace        | Miss Type                                |
| ---- | ----------- | --------------- | ------------------------- | ---------------------------------------- |
| 1    | 0b0000 0100 | …0000 / 0 / 100 | M (compulsory)            | compulsory                               |
| 2    | 0b0000 0101 | …0000 / 0 / 101 | H (same I, T as 1)        |                                          |
| 3    | 0b0110 1000 | …0110 / 1 / 000 | M (compulsory)            | compulsory                               |
| 4    | 0b1100 1000 | …1100 / 1 / 000 | M (compulsory)            | compulsory                               |
| 5    | 0b0110 1000 | …0110 / 1 / 000 | H (same I, T as 3)        | conflict                                 |
| 6    | 0b1101 1101 | …1101 / 1 / 101 | R (compulsory, replace 4) | compulsory                               |
| 7    | 0b0100 0101 | …0100 / 0 / 101 | M (compulsory)            | compulsory                               |
| 8    | 0b0000 0100 | …0000 / 0 / 100 | H (same I, T as 1)        | capacity (fully associative also misses) |
| 9    | 0b1100 1000 | …1100 / 1 / 000 | R                         | capacity (just replaced)                 |

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

| Tag (T/I)     |      |
| ------------- | ---- |
| 00000 → 01000 | ~    |
| 01101 → 11001 | ~    |
| 11001 → 00000 | ~    |
| 11011         | ~    |

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

**AMAT = Hit Time + Miss Rate * Miss Penalty**

- **Hit time:** the time for the cache to verify our data exists in the cache
- **Miss Penalty:** the time taken to get our data from memory (or the next level cache) when we miss
- **Miss Rate:** the number of accesses that missed at that level / total number of accesses…
  1. Global: *to the cache system*
  2. Local: *to the cache level*

<u>Improve AMAT:</u>

1. Decreasing cache "Hit time"
2. Reduce miss rate
3. Reduce miss penalty

Example





problems 4, 6