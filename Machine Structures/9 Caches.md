# Caches

2^XY^ means

| X = 0     | ---          | Y = 0     | 1       |
| --------- | ------------ | --------- | ------- |
| **X = 1** | kibi ~10^3^  | **Y = 1** | **2**   |
| **X = 2** | mebi ~10^6^  | **Y = 2** | **4**   |
| **X = 3** | gibi ~10^9^  | **Y = 3** | **8**   |
| **X = 4** | tebi ~10^12^ | **Y = 4** | **16**  |
| **X = 5** | pebi ~10^15^ | **Y = 5** | **32**  |
| **X = 6** | exbi ~10^18^ | **Y = 6** | **64**  |
| **X = 7** | zebi ~10^21^ | **Y = 7** | **128** |
| **X = 8** | yobi ~10^24^ | **Y = 8** | **256** |
|           |              | **Y = 9** | **512** |

## T / I / O

**Tag:** Used to distinguish different blocks that use the same index

- num bits = # bits in memory address - Index Bits - Offset Bits

**Index:** The set that this piece of memory will be placed in

- num bits = log2 (# of indices)

**Offset:** The location of the byte in the block

- num bits = log2 (size of block)

*log2(memory size) = address bit-width = # tag bits + # index bits + # offset bits*

**cache size = block size * num blocks**

## Cache Misses

**Compulsory:** first time you ask the cache for a certain block

- reduce by having longer cache lines (bigger blocks)

**Conflict:** if hypothetically, you went through the ENTIRE string of accesses with a fully associative cache and wouldn't have missed

- increasing associativity or improving the replacement policy would remove the miss

**Capacity:** if hypothetically, you ran the ENTIRE string of memory accesses with a fully associative cache of the same size as your cache, and it was a miss for that specific access

- remove this miss by increasing cache capacity

