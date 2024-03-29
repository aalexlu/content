# Number Representation

## Unsigned Integers

### Conversions

|            | Decimal | Binary | Hex  |
| ---------- | ------- | ------ | ---- |
| 0b10010011 | 147     | -      |      |
| 63         | -       |        |      |
| 0b00100100 |         | -      |      |
| 0          | -       |        |      |
| 39         | -       |        |      |
| 437        | -       |        |      |
| 0x0123     |         |        | -    |

## IEC Prefixing System:

| Ki (Kibi) | Mi (Mebi) | Gi (Gibi) | Ti (Tebi) | Pi (Pebi) | Ei (Exbi) | Zi (Zebi) | Yi (Yobi) |
| --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- |
| 2^10      | 2^20      | 2^30      | 2^40      | 2^50      | 2^60      | 2^70      | 2^80      |

Examples:

| Number   | IEC Prefix | Number   | IEC Prefix | Number   | IEC Prefix | Number   | IEC Prefix |
| -------- | ---------- | -------- | ---------- | -------- | ---------- | -------- | ---------- |
| **2^16** | 2^6 Kibi   | **2^27** | 2^7 Mebi   | **2^43** | 2^3 Tebi   | **2^36** | 2^6 Gibi   |
| **2^34** | 2^4 Gibi   | **2^61** | 2^1 Exbi   | **2^47** | 2^7 Tebi   | **2^59** | 2^9 Pebi   |

| IEC Prefix | Number              | IEC Prefix | Number | IEC Prefix | Number |
| ---------- | ------------------- | ---------- | ------ | ---------- | ------ |
| **2 Ki**   | (2^1 * 2^10) = 2^11 | **512 Ki** | 2^19   | **16 Mi**  | 2^24   |
| **256 Pi** | (2^3 * 2^50) = 2^58 | **64 Gi**  | 2^36   | **128 Ei** | 2^67   |

## Signed Integers

|            | Largest | Adding 1      | 0        | 1        | -1       | -17      | 17       |
| ---------- | ------- | ------------- | -------- | -------- | -------- | -------- | -------- |
| Unsigned   | 255     | back to 0     | 00000000 | 00000001 | n/a      | n/a      | 00010001 |
| Biased     | 128     | 0-127 = 127   | 01111111 | 10000000 | 01111110 | 01101110 | 10010000 |
| Two's Comp | 127     | (-2)^7 = -128 | 00000000 | 00000001 | 11111111 | 11101111 | 00010001 |

Normal bias for 2 bits: 2^n-1^ - 1 for N bits

## Two's Complement

cannot overflow

