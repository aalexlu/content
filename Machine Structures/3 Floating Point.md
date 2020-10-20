# Floating Point

- large range of values, high precision, real arithmetic results
- as you move away from 0, precision goes down
- not associative

Binary representation for floating point values

- **sign:** 0 for positive, 1 for negative
- **exponent:** in biased notation
- **significand / mantissa:** unsigned integers to store a fraction

### Single Precision 32-bit

| 1    | 8        | 23                            |
| ---- | -------- | ----------------------------- |
| Sign | Exponent | Mantissa/Significand/Fraction |

**Normalized floats:**

- (-1)^*Sign* * 2^*(Exp + Bias)* * 1.significand

**Denormalized floats:**

- (-1)^*Sign* * 2^*(Exp + Bias **+ 1**)* * 0.significand

| Exponent | Significand | Meaning  |
| -------- | ----------- | -------- |
| 0        | Anything    | Denorm   |
| 1-254    | Anything    | Normal   |
| 255      | 0           | Infinity |
| 255      | Nonzero     | NaN      |

## Conversions

largest finite positive value:

smallest positive value:

smallest positive normalized value:

next smallest number larger than 2:

next smallest number larger than 4:

**stepsize:**

| Decimal     | Binary         |
| ----------- | -------------- |
|             | **0x00000000** |
| **8.25**    |                |
|             | **0x00000F00** |
| **39.5625** |                |
|             | **0xFF94BEEF** |
| **neg inf** |                |

​	